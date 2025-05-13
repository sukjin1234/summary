### 라즈베리파이 한글 버전 설치
```Linux
sudo apt-get install fonts-unfonts-core -y
sudo apt-get install ibus ibus-hangul -y
sudo reboot
```

---

## telegram bot 
```
git clone https://github.com/python-telegram-bot/python-telegram-bot
```

---

## 카메라로 사진 찍어서 화면에 보여주는 코드
```python
import cv2
import sys
import time

cap = cv2.VideoCapture(0)
cap.set(cv2.CAP_PROP_FRAME_WIDTH, 640)
cap.set(cv2.CAP_PROP_FRAME_HEIGHT, 480)
if not cap.isOpened():
  print("camera open error")
  exit()

while True:
  ret, image = cap.read() # ret에 이미지가 읽어졌는지 알려줌
  if not ret:
    print("frame read error")
    break
  cv2.imshow('CAMERA', image)
  if cv2.waitKey(1)&0xFF == ord('q'):
    break

  time.sleep(10) # 10초 동안 쉼
  cv2.imwrite('image.jpg', image) # image를 image.jpg로 저장함

cap.release()
cv2.destroyAllWindows()
```

---

> python-telegram-bot/examples/timerbot.py
## 실제 코드에 takePhoto 메소드(사진 찍는 코드) 적용한 코드
```python
#!/usr/bin/env python
# pylint: disable=unused-argument
# This program is dedicated to the public domain under the CC0 license.

"""
Simple Bot to send timed Telegram messages.

This Bot uses the Application class to handle the bot and the JobQueue to send
timed messages.

First, a few handler functions are defined. Then, those functions are passed to
the Application and registered at their respective places.
Then, the bot is started and runs until we press Ctrl-C on the command line.

Usage:
Basic Alarm Bot example, sends a message after a set time.
Press Ctrl-C on the command line or send a signal to the process to stop the
bot.

Note:
To use the JobQueue, you must install PTB via
`pip install "python-telegram-bot[job-queue]"`
"""

import logging
import cv2 '''필요한 라이브러리 (cv2, sys, time)'''
import sys 
import time 
from telegram import Update
from telegram.ext import Application, CommandHandler, ContextTypes

# Enable logging
logging.basicConfig(
    format="%(asctime)s - %(name)s - %(levelname)s - %(message)s", level=logging.INFO
)
# takePhoto method : 카메라로 찍은 사진 저장해줌
def takePhoto():
  cap = cv2.VideoCapture(0)
  cap.set(cv2.CAP_PROP_FRAME_WIDTH, 640)
  cap.set(cv2.CAP_PROP_FRAME_HEIGHT, 480)
  if not cap.isOpened():
    print("camera open error")
    return
  ret, image = cap.read() # ret에 이미지가 읽어졌는지 알려줌
  if not ret:
    print("frame read error")
    return
  cv2.imshow('CAMERA', image)
  time.sleep(1)
  cv2.imwrite('image.jpg', image) # image를 image.jpg로 저장함
  
  cap.release()
  cv2.destroyAllWindows()

# Define a few command handlers. These usually take the two arguments update and
# context.
# Best practice would be to replace context with an underscore,
# since context is an unused local variable.
# This being an example and not having context present confusing beginners,
# we decided to have it present as context.
async def start(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    """Sends explanation on how to use the bot."""
    await update.message.reply_text("Hi! Use /set <seconds> to set a timer")


async def alarm(context: ContextTypes.DEFAULT_TYPE) -> None:
    """Send the alarm message."""
    # takePhoto() 실행
    takePhoto() 
    job = context.job
    await context.bot.send_message(job.chat_id, text=f"Beep! {job.data} seconds are over!")
    # 사용자에게 사진을 보내줌
    await context.bot.sendPhoto(job.chat_id, photo=open('./image.jpg','rb') 


def remove_job_if_exists(name: str, context: ContextTypes.DEFAULT_TYPE) -> bool:
    """Remove job with given name. Returns whether job was removed."""
    current_jobs = context.job_queue.get_jobs_by_name(name)
    if not current_jobs:
        return False
    for job in current_jobs:
        job.schedule_removal()
    return True


async def set_timer(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    """Add a job to the queue."""
    chat_id = update.effective_message.chat_id
    try:
        # args[0] should contain the time for the timer in seconds
        due = float(context.args[0])
        if due < 0:
            await update.effective_message.reply_text("Sorry we can not go back to future!")
            return

        job_removed = remove_job_if_exists(str(chat_id), context)
        context.job_queue.run_once(alarm, due, chat_id=chat_id, name=str(chat_id), data=due)

        text = "Timer successfully set!"
        if job_removed:
            text += " Old one was removed."
        await update.effective_message.reply_text(text)

    except (IndexError, ValueError):
        await update.effective_message.reply_text("Usage: /set <seconds>")


async def unset(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    """Remove the job if the user changed their mind."""
    chat_id = update.message.chat_id
    job_removed = remove_job_if_exists(str(chat_id), context)
    text = "Timer successfully cancelled!" if job_removed else "You have no active timer."
    await update.message.reply_text(text)


def main() -> None:
    """Run bot."""
    # Create the Application and pass it your bot's token.
    application = Application.builder().token("TOKEN").build()

    # on different commands - answer in Telegram
    application.add_handler(CommandHandler(["start", "help"], start))
    application.add_handler(CommandHandler("set", set_timer))
    application.add_handler(CommandHandler("unset", unset))

    # Run the bot until the user presses Ctrl-C
    application.run_polling(allowed_updates=Update.ALL_TYPES)


if __name__ == "__main__":
    main()
```

---

### 코드 설명
| | |
|---|---|
| import cv2 | 영상 처리에 필요한 python 라이브러리 |
| TOKEN 연결하는법 | `application = Application.builder().token("TOKEN").build()` TOKEN 부분에 부여받은 token 입력 |
| 나만의 메소드 불러오는 방법 | main() 메소드에 `application.add_handler(CommandHandler("Message", method))` 추가 <br> 채팅으로 /Message를 보냈을 때 등록한 method 실행 |
