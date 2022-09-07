import streamlit as st
import requests

API_key = "67f27fbe9b4da00df49eb2ec0cf708f8"                                         #signed in to get api key from openweathermap
def find_weather(city):
    st.write("Cityname is ",city)
    url=f"https://api.openweathermap.org/data/2.5/weather?q={city}&appid={API_key}"  # f to avoid brackets
    weather_data = requests.get(url).json()                                          #pull weather data
    #st.json(weather_data)                                                           # to check json data
    general = weather_data['weather'][0]['main']                                     #refer json

    icon_id = weather_data['weather'][0]['icon']
    icon = f"http://openweathermap.org/img/wn/{icon_id}@2x.png"
    temperature = round(weather_data['main']['temp'])                               #round figure
    return general,temperature,icon


def main():
    st.header("Weather app")
    city=st.text_input("Enter the city name : ")
    if st.button("Find"):
        general,temperature,icon=find_weather(city)
        st.metric(label="Temperature", value=f"{temperature}°C")                    # metric to display larger nums
        #st.write(temperature,"°C")
        st.write("Temperature: ",general)
        st.image(icon)
