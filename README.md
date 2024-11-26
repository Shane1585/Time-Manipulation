<h1>Time Reversal Plugin User Guide</h1>

<h2>What does this plugin do?</h2>
<p>This is a plugin to reverse actors to a previous location and velocity in time, with the ability to play this location history back at variable speeds and to stop at any point while reversing.</p>
<p>You can reverse anything by tag, or individual actors/characters. You can trigger an actor to begin recording on game start, while crossing boundaries, or in any other custom way.</p>

<h2>Requirements</h2>
<p>To use the example level, this plugin relies on the provided university GAD2010 Base Project/Plugin, as it uses the provided character in the example.</p>

<h2>How to install</h2>
<p>Download or clone the project. Copy the TimeManipulation folder to your plugins folder in your project.</p>
<img src="https://github.com/Shane1585/Time-Manipulation/blob/main/ReadMeImages/InstallLocation.png">

<p>If the project contains the base project for the university module, you can load a preview map that will explain further how the plugin works and how to use it:</p>
<img src="https://github.com/Shane1585/Time-Manipulation/blob/main/ReadMeImages/PreviewMap.png">

<p>Please note that with the preview map, some areas have start/stop recording zones, and skipping ahead by moving the character to a certain room may not trigger these recording events (and might cause issues with the tutorial)</p>

<h2>Component/Blueprint Guide</h2>
<h3>BP_TimeReverse</h3>
<p>Add this to any object or character that you would like to be reversible. To do this, add this component to the actor, and then set the following variables depending on preference:</p>
<img src="https://github.com/Shane1585/Time-Manipulation/blob/main/ReadMeImages/BP_TimeReverse.png">
<ul>
  <li><b>Frames -</b> This is how the component stores the location and velocity history. You can pre-set these to give a recording of the location prior to the game starting. This allows you to pre-add some location and velocity history (this would be useful for scripted events).</li>
  <li><b>Is Recording? -</b> Whether or not the actor is currently recording transform and velocity history. Warning: When starting recording off of custom events, you should use the <b>StartNewRecording</b> function to start an object recording, instead of setting this directly</li>
  <li><b>Is Reversing? -</b> Whether or not the actor is currently reversing. Warning: When starting reversing, you should use the <b>StartRewind</b> function instead of setting this directly.</li>
  <li><b>Max Time Recording when Stopped -</b> This is how long the item is recorded as having stayed in one place. For example, if the item was stood still for 10 seconds, setting this to 0.2 would only record the first 0.2 seconds of being stationary. This is useful to avoid long pauses when reversing. To effectively disable this behaviour, you may set this to a high value, such as 999,999.</li>
  <li><b>Reverse Speed -</b> This is how fast your character will reverse. This is set upon calling the start rewind function, however, this may be modified while rewind is in progress.</li>
  <li><b>Starts Off Recording -</b> This determines whether the actor will start recording on game start.</li>
  <li><b>Play Reverse Animation -</b> en reversing a character, this determines whether or not the reverse montage is played when reversing the character.</li>
  <li><b>Reverse Montage -</b>  This is the montage played while a character is reversing, if play reverse animation is set to True.</li>
</ul>

<h3>BP_TimeReverseUI</h3>
<p>Add this component to the player character, to enable a selection wheel/radial menu that presents some options for the player to select, for how to reverse. (This UI may not fit within the ICA). This object requires a <b>BP_TimeManager</b> to exist in the map, as this UI reverses objects by group (enabled by BP_TimeManager).</p>

<h3>Start and Stop Recording Options</h3>
<img src="https://github.com/Shane1585/Time-Manipulation/blob/main/ReadMeImages/TimeGates.png">
<p>Some basic blueprint classes exist to enable starting and stopping recording on actors that have overlapped with collision boxes in these blueprints. These would be useful for enabling recording only when entering certain areas.</p>
<p>The stop recording gate can be set to stop all objects, or only those that have passed it from recording. The start gate can be set to start all objects in passed in trigger volumes recording when the player passes it, or can be set up only to start those objects that have passed it, recording. Note: To use the trigger volume option, actors must be set up with the generate overlap events box ticked.</p>

<h3>BP_TimeManager</h3>
<p>This actor acts as a way to coordinate multiple time-reversing objects. You can choose to use time reversing objects without this, however you will need to trigger them individually, rather than as a group. This also allows for screen effects to be used when reversing, if passed a post process volume.</p>
UE5.4 University project - Blueprint plugin allowing for moving actors backwards to previous transforms and velocities

<h2>Troubleshooting</h2>
<ul>
  <li>To avoid an issue with the appearance of lag while the player is reversing, disable camera lag on the spring arm of the character.</li>
  <li>To avoid trigger boxes used by the start gate not working, please make actors inside of the boxes that you intend to start recording, set up to generate overlap events. Without this, trigger boxes cannot detect overlapping actors to start the recording.</li>
  <li>To be able to use the example map, please add the plugin to the base project, as it uses the provided example character as a base to build on.</li>
</ul>
