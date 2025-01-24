
Windows creating a window takes two steps first the Creation and then the events handling.


The creation is pretty self explanatory its just opening a window with the desired properties but Events is a bit more complicated I will come back to that later on when at that stage



Windows creation comes in two parts both Events and Window, Events are handled using something called messages, these messages are sent when an event occurs and we can get the events by using two methods, theres the get message function and the peak message function These have the same purpose but the difference is the get message function wait till a message is sent if there are none and the peak message just continues if no messages were found. 


GetMessage: 
" Get a message and wait for the next one if you cant find any"


PeekMessage:
" Get a message but continue if you can not find any"


We will use PeekMessage so we can keep executing code without waiting for a message when we have a message we have to send it thru something called the window procedure which is done using a function called dispatch message the window procedure is a function that we define ourself with basically handles the message  so we will get info ab key presses


![[Screenshot 2024-10-02 214516.png]]


	HINSTANCE = m_hInstance;
	HWND = m_HWnd


these H instance and H window are needed when the window is connected to the actual window instance

the hwindow is connected to the actual window instance and the hinstance is more connected to the application 