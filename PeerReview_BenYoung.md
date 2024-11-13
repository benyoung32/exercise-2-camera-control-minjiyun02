# Code Review for Programming Exercise 2 #
## Solution Assessment ##

Note for all stages: When I first opened the project, all but one of the cameras were improperly setup in the scene. Each was set ontop of the vessel and were facing forwards, not downwards toward the ground. It's possible I made a mistake while importing/running the project so I will just mention it here. Also, for all camera's the draw logic appears to be implemented in code, but I do not see any indicators while running the project

### Stage 1 ###

- [ ] Perfect
- [ ] Great
- [x] Good
- [ ] Satisfactory
- [ ] Unsatisfactory

#### Justification ##### 
The camera is locked perfectly on the X and Z axes, but I am unable to see the vessel, and can only see the shadow. This is due to the camera being set to the vessel's position, without calling the CameraControllerBase _process super method which would adjust the Y value to be the correct distance from the ship determined by the current zoom level.
### Stage 2 ###

- [ ] Perfect
- [ ] Great
- [ ] Good
- [ ] Satisfactory
- [x] Unsatisfactory

#### Justification ##### 
The camera scrolls correctly, but I am unable to move the vessel while this camera is active. This is likely due to the code which is meant to keep the vessel within the camera frame
### Stage 3 ###

- [ ] Perfect
- [ ] Great
- [ ] Good
- [x] Satisfactory
- [ ] Unsatisfactory

#### Justification ##### 
This camera has the same issue as the position lock, where the y coordinate is not adjusted properly. Additionally, the catch up system is never able to exactly match the vessel's position, instead it repeatedly overshoots the vessel which results in a shaking motion. The leash distance works, however it is set very wide by default and the vessel is able to leave the screen vertically (at least on my display)
### Stage 4 ###

- [ ] Perfect
- [ ] Great
- [x] Good
- [ ] Satisfactory
- [ ] Unsatisfactory

#### Justification ##### 
Same y-position and shaking issue as above. The lead speed is rather fast, while the catchup speed is rather slow. Combined this makes the camera somewhat uncomfortable to use, but it does otherwise meet the requirements.

### Stage 5 ###
- [ ] Perfect
- [ ] Great
- [ ] Good
- [ ] Satisfactory
- [x] Unsatisfactory

#### Justification ##### 
Not sure if I imported the project incorrectly, but this camera does not seem to work for me. Looking at the code, it seems like it should work, so I am not sure what the issue is. 

## Code Style ##

### Code Style Infractures ###
Some lines of code are very long, e.g. `position_lock.gd:34` and `push_box.gd:77`

## Best Practices ##

### Best Practice observations ###

I like the way the project splits up complex or reusable logic into separate functions, e.g. `four_way_speedup.gd:draw_box()` and `is_in_zone()`. I think this is a good way to manage complexity in the later stages of this project which require a lot of behavior at once from the script. 

Some camera functions call the super method, while some do not. In general when using inheritance, it's best to clearly define the role of the base class, which in this case is operating as an abstract class, and the child class. The base class should be responsible for behavior common to all child classes, such as setting the y-position or calling the draw_logic() function when necessary. This inconsistency is likely the cause of several major bugs in the project.