## 17 - 18 August : flow chart and sketch diagram in AI
considered the entire flow of the game and how players interact with the screen. As a result of doing more in-depth research and thinking about the sensor and Unity interaction part of the game, I had to change some of the game mechanics, and the in-game UI.
- Level 3: __Chinese character formation in a grid using sections.__ “森” or “晖”&“晕”？ and how to interact? (The idea so far is to have three sensors on the top left and right for selecting text relative to the position on the screen. But i can only do "confirmation" like clicking instead of "selection" like computer mouse movement)  ___I need to check with Mahalia___
- Level 4: __horizontal board game.__ aiming to encourage players to practice speaking Chinese. players need to read specific Chinese sentences and control the game character to move smoothly. ___game map references some voice-activated games___
### physical prototype and game flow chart:

![Sketch_画板 1](https://github.com/YiningJenny/FinalYearProject/assets/119497753/b972b862-32c6-4234-bdbc-3966702479b5)
![Sketch-02](https://github.com/YiningJenny/FinalYearProject/assets/119497753/875b9f0b-e268-46cb-a33e-9a83c025a62d)

## 4th October - CCI symposium

- prototype of my new level:
  
![image](https://github.com/YiningJenny/FinalYearProject/assets/119497753/ef818751-abf4-4463-9aa3-c13e0675a38c)

- Audience testing:
  
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
## 9th Oct
Reschedualed my timetable. I realized that I cant really arrange till the last day. So I moved my plans up.
![image](https://github.com/YiningJenny/FinalYearProject/assets/119497753/892e3335-c871-4e9f-b249-ebac581fe7aa)
## 12th Oct - tutorial with Mahalia
I was kinda stuck on the core gameplay machanics. Mahalia suggestted me go back the original game goal and do a recap.
- Think about my target audience
  - My opinion was __'people who interested in language learing'__. Mahalia prefer to be open-minded and not that serious: language learning can be in another way, no class constraints. Compared with education, my project is more game based, so it's better for me to target my audience into __'people who interest in language'__
- To recap the story of my inspiration, tower babel. The first generation of the physical game was a brilliant way to convey the existence of language barriers. The second digital generation emphasises the importance of collaboration. Additionally, both generations of the game are co-operative multiplayer. However, due to time constraints, we removed all co-operative elements in the third generation. Now, I can reintroduce co-operation in the fourth generation because in the story of Tabapet, those who tried to co-operate to build a tower in case of a second flood were punished by the gods. "collaboration" and "language" can be the two core machanics in my game. The mode of cooperation ccan be:
  - digital - two players chase each other in the game
  - physical - one player conduct and another operate
 
## 17th Oct - start Unity level design

- Sketch of the two version and some of the Hanzi components that I want to use.

![第四关关卡设计草稿](https://github.com/YiningJenny/FinalYearProject/assets/119497753/9022e3b3-3b8a-460a-a9eb-1005f42448c6)

- another unfinished version of new level: I followed the method of disassembling the kanji into different parts and lowering the colour contrast of the fonts for the game background. Both on top and bottom of the screen, I used the 'spikes' word from Chinese hieroglyphics. Since Chinese hieroglyphics is more based on image, I except audience can recognize the meaning of the word by its shape. I also plan to apply more hieroglyphics to my game in this way.

![新版第四关](https://github.com/YiningJenny/FinalYearProject/assets/119497753/4c0745ea-d2fc-410b-bdb0-e8412fee8694)
![image](https://github.com/YiningJenny/FinalYearProject/assets/119497753/1ff41d16-759f-41c8-8795-b1a567dbdf72)

I will keep both of the two version for inviting people play my game, and do further adaptation.
