# Text Entry Data from the real world

This repository contains two datasets from real-life use of MaxieKeyboard, a virtual QWERTY keyboard for Android.

MaxieKeyboard was installed on users' smartphones as a complete replacement for the standard keyboard. Each user participated for a variable time period. We logged keystrokes and related metrics during all kinds of text entry contexts, excluding however text entry in password, numeric, email and url fields. For extra privacy, Dataset 2 didn't record anything related to keystrokes apart from finger slippage (difference between key down and key up coordinates) and interkey intervals.

## Datasets
### Dataset 1
Contains data from 3 young and 4 older adults, collected for a period starting 09/2014. The keyboard did not incorporate any support for text entry (e.g. autocorrect).
### Dataset 2 
Contains data from 12 young adults, collected for a period starting 02/2016. This version of the keyboard included more advanced features (see field descriptors for session tables).

## Data Tables

Each dataset consists of two tables with some (or all) of the following fields:

### sessions_xxx
A “session” begins when the keyboard appears on the screen and when it is hidden. Some applications cause a “keyboard show” event to occur, even if the keyboard is not actually shown, hence you may observe zero typing events for these. Typically such sessions have a “width” and “height” data value of zero (because the keyboard was not actually drawn).

#### Data fields
- id (int): the session id
- session_width (int): the keyboard width in pixels
- session_height (int): the keyboard height in pixels
- start_time (int): timestamp of when the session began
- end_time (int): timestamp of when the session ended
- app (text): application name or package name in which this session took place
- low_errors (int): number of minor spelling mistakes in this session
- high_errors (int): number of major spelling mistakes in this session
- suggestions_picked (int): number of picked suggestions in this session
- injections (int): number of errors injected in this session (this wasn't used during data collection)
- first_word (text): the first word entered in this session
- autocorrect (int): the user had the autocorrect option enabled or not
- sound (int): auditory feedback was on/off - one beep for a slight typing error, two beeps for a serious one
- haptic (int): tactile feedback was on/off - one vibration for a slight typing error, two vibrations for a serious one
- visual (int): visual feedback was on/off - yellow highlighting of typing errors, red for serious ones, orange for autocorrects. A coloured line between the suggestion bar and first row of keys also lit up in corresponding colour.
- sugg_highlights (int): visual feedback was on/off - if on, words in the text that were picked from the suggestion bar were highlighted blue
- dots (int): circles appearing on touch locations and fading as more touches were added, showing touch history
- user (int): an id for the user that created the session
- age (char): Y=young adult, O=older adult
  
### typing_events_xxx
All the keyboard typing events recorded during use.

#### Data fields
- id (int): an id for the event
- sessionid (int): the id of the session in which this event took place
- user (int): id of the user who generated this event
- timesincelast (int): elapsed time in milliseconds between this and the previous input event belonging to the same session
- duration (int): elapsed time in milliseconds between the key_down and key_up events of this input event
- rawxdown (double): screen X coordinates of the key_down event
- rawydown (double): screen Y coordinates of the key_down event
- rawxup (double): screen X coordinates of the key_up event
- rawyup (double): screen Y coordinates of the key_up event
- xdown (double): keyboard area X coordinates of the key_down event
- ydown (double): keyboard area Y coordinates of the key_down event
- xup (double): keyboard area X coordinates of the key_up event
- yup (double): keyboard area Y coordinates of the key_up event
- minoraxisdown (double): minor axis of the touch ellipse area in the key_down event
- majoraxisdown (double): major axis of the touch ellipse area in the key_down event
- minoraxisup (double): minor axis of the touch ellipse area in the key_up event
- majoraxisup (double): major axis of the touch ellipse area in the key_up event
- rawxdiff (double): difference in X coordinates of the key_down and key_up event, calculated from screen coords
- rawydiff (double): difference in Y coordinates of the key_down and key_up event, calculated from screen coords
- xdiff (double): difference in X coordinates of the key_down and key_up event, calculated from keyboard area coords
- ydiff (double): difference in Y coordinates of the key_down and key_up event, calculated from keyboard area coords
- keycode (int): raw key code of the input event
- keychar (text): character corresponding to the input event (note, keycode==-5 && keychar==NULL => backspace)
- followspace (int): 0 or 1 depending on whether this event follows a space_bar character
- precedespace (int): 0 or 1 depending on whether this event preceded a space_bar character
- followshift (int): 0 or 1 depending on whether this event follows a press of the shift key
  
## Attribution

If using this data, please cite:

Andreas Komninos, Mark D. Dunlop, Kyriakos Katsaris and John Garofalakis. 2018. A glimpse of mobile text entry errors and corrective behaviour in the wild, In Proc. Extended Abstracts, Mobile HCI'18, Barcelona, Spain. ACM. DOI: https://doi.org/10.1145/3236112.3236143.

Andreas Komninos, Emma Nicol and Mark D. Dunlop. 2015. Designed with Older Adults to Support Better Error Correction in SmartPhone Text Entry: The MaxieKeyboard, In Proc. Adjunct proc. of the 17th International Conference on Human-Computer Interaction with Mobile Devices and Services, Copenhagen, Denmark. ACM. DOI: https://doi.org/10.1145/2786567.2793703

Andreas Komninos, Kyriakos Katsaris, Emma Nicol, Mark D. Dunlop and John Garofalakis. 2020. Mobile Text Entry Behaviour in Lab and In-the-Wild studies: Is it different?, arXiv:2003.06323 [cs.HC] https://arxiv.org/abs/2003.06323
