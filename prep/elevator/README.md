# Build an elevator system using pseudo language

Elevator Details

The basic elevator machinery is completely dumb (it doesn't do anything it's not told to do) but is capable of interpreting and executing the commands:

"open elevator door"
"close elevator door"
"go up full speed"
"go down full speed"
"slow down"
"stop"
...and it accepts user input in the form of:

floor buttons inside the elevator
door open and close buttons inside the elevator
up and down call buttons on each floor
...and it has sensors for:

if a human is in the door closing path
if it is currently at a floor (instead of in-between floors)
...and it has a few quirky requirements:

it must "slow down" at least 1 floor before it stops.
there is a small chance that it actually stops between floors by accident (it's an old elevator)

```
PROGRAM Elevator:
    While running
      Upper floor call
        GoUpWhenUpperFloorButtonClicked If CheckIfFree
        SlowDownIfNecessary
        OpenTheDoorWhenSafe
        CloseDoorWhenSafe
      Down floor call
        GoDownWhenUpperFloorButtonClicked If CheckIfFree
        SlowDownIfNecessary
        OpenTheDoorWhenSafe
        CloseDoorWhenSafe
      CallEmergency
    End
END

PROGRAM CloseDoorWhenSafe
  If no human in the door closing path And the door is not Closed
  Close the door
END

PROGRAM OpenTheDoorWhenSafe
  If the elevator is not at the middle of the floor And the door is closed
  Open the door
End

PROGRAM StopWhenDestinationArrived
  If the floor number matches the user clicked number
  Stop the elevator
End

PROGRAM GoUpWhenUpperFloorButtonClicked
  If the number of the clicked button larger than the current elevator number
  Go up full speed
End

PROGRAM GoDownWhenUpperFloorButtonClicked
  If the number of the clicked button smaller than the current elevator number
  Go down full speed
End

PROGRAM CallEmergency
  If stopped in the middle between floors.
  Dial emergency number
End

PROGRAM CheckIfFree
  If the door is closed and the speed is zero
    Elevator free
  ELSE
    Elevator not Free
  End
End


PROGRAM SlowDownIfNecessary
  IF we are traveling up at full speed
    IF we are only 1 floor away from the lowest destination floor
      slow down
    END
  ELSE IF we are traveling down at full speed
    IF we are only 1 floor away from the highest destination floor
      slow down
    END
  END
END
```
