# obhavo
import requests 
import telebot 
import json   

token='726606764:AAGvL69oWVlNZrv9uknwrQh2EuncSIT-ysg'  

bot=telebot.TeleBot(token)  

@bot.message_handler(commands=['start']) 
def start(message):     
    bot.send_message(message.chat.id, '@vahimachi_bot ga hush kelibsiz. Shahar nomini kiriting.(Faqat inglizchada)')   
    
@bot.message_handler(content_types=['text']) 
def weather(message):     
    api_url='https://api.openweathermap.org/data/2.5/weather'     
    city=message.text     
    r=requests.post(url=api_url, params={'q':city, 'APPID':'35897244bed48a9ea34419924a355e3e', 'units':'metric'})     
    if r.status_code==200:          
      
      response=json.loads(r.content)         
      temp=str(response['main']['temp'])         
      max_temp=str(response['main']['temp_max'])         
      min_temp=str(response['main']['temp_min'])         
      wind_speed=str(response['wind']['speed'])         
      pressure=str(response['main']['pressure'])         
      humidity=str(response['main']['humidity'])          
      
      msg='Hozirgi vaqtda siz so`ragan shaharda' ' ' +temp+'daraja '+'\n'+'Yuqori temperatura '+max_temp+' daraja'+'\n'+' Past temperatura'+min_temp+' daraja'+'\n'+wind_speed+'\n'+pressure+'\n'+humidity+'\n'          
      bot.send_message(message.chat.id, msg)     
    else:         
      bot.send_message(message.chat.id, 'Og`ayni xato diyaptiku. Boshqa kiritib ko`ringchi') 
bot.polling(none_stop=True)
