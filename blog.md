## 17 - 18 August : flow chart and sketch diagram in AI
considered the entire flow of the game and how players interact with the screen. As a result of doing more in-depth research and thinking about the sensor and Unity interaction part of the game, I had to change some of the game mechanics, and the in-game UI.
- Level 3: __Chinese character formation in a grid using sections.__ “森” or “晖”&“晕”？ and how to interact? (The idea so far is to have three sensors on the top left and right for selecting text relative to the position on the screen. But i can only do "confirmation" like clicking instead of "selection" like computer mouse movement)  ___I need to check with Mahalia___
- Level 4: __horizontal board game.__ aiming to encourage players to practice speaking Chinese. players need to read specific Chinese sentences and control the game character to move smoothly. ___game map references some voice-activated games___
### physical prototype and game flow chart:

![Sketch_画板 1](https://github.com/YiningJenny/FinalYearProject/assets/119497753/b972b862-32c6-4234-bdbc-3966702479b5)
![Sketch-02](https://github.com/YiningJenny/FinalYearProject/assets/119497753/875b9f0b-e268-46cb-a33e-9a83c025a62d)

## 4th October - CCI symposium
![3d1b878bdee144ff4c64af7f7f74178](https://github.com/YiningJenny/FinalYearProject/assets/119497753/56bc6b70-0dfb-4eb4-aeaf-f89fce1a67b0)

- The second generation was not really related to language.
- The horizontal board games does not really make sense. (My prototype was not arduino based, so it was super simple to control by keyboard. The main character was designed by the meaning of person, that also not easy to tell.). If it's a voice controlled game, the level is fine. Maybe I can try endless platform running game, the arduino controlling would be much more easier with single induction.
- The grid word components combinition not really worked, they need someone to explain.
- make more depth of field. more lighting effects (leave it if I have more time)
- other thoughts about level design: dialogues with sentences that have several meanings, and the players can decide how the plot goes.
generally, all of them being more interested in Chinese learning, and the painting-based characters also make sense to them. Instead of serious language education, its more like a portal of Chinese learning.
- Generally, the audience prefer to be actively involved in the educational process and not simply be passive listeners and onlookers. Even though I was talking about game design elements which totally related to my practice part, almost all of them were scrolling. Maybe it's easier for people nowadays to accept digital information rather than purely text. (I will add it to my question list)

I also rescheduled my timetable:
![gantt chart](https://github.com/YiningJenny/FinalYearProject/assets/119497753/0566f498-01db-4763-bca3-00acaa468f27)

## 5th October - Toturial with Mahalia and Lieven
Mahalia's feedback: 
- The Level 1 character models are kind of blurred by the background. It lookd a little bit confusing, (maybe make people feel confused is my goal)but I'd better make the model more stand up from the background.
- We talked about game's core mechanics, she suggested me to talk to Lieven about the technical fundamentals.
- about dissertation: write pieces of paragraphs in daily, then I can organize them easily in the future.

Lieven's suggestion:
  - For speech recognition, I can try the following tutorials:
    - [google Speech-to-Text API](https://codelabs.developers.google.com/codelabs/cloud-speech-text-csharp#0)
    - [Microsoft Speech recognition engine class](https://learn.microsoft.com/en-us/dotnet/api/system.speech.recognition.speechrecognitionengine?view=netframework-4.8.1)
- For hand motion track, I can try:
  - camera
  - kinect (borrow one from CCI)
  - or leap motion
- For Arduino wireless, I can try:
  - [Bluetooth HC-05](https://www.deviceplus.com/arduino/how-to-control-an-arduino-from-a-windows-computer/)
Overall, the good news is that I don't need to use Arduino in the new levels, so need to worry the digital sending efficiency. 
