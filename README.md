# PULLED ROPE GENERATOR 

###### NORCAT || Brandon Cotesta || Version 0.1.1

This tool was designed to make the process of generating pulled cable along a cable tray easier.
While it does generate all the necessary gameobjects, you still need to manually move the checkpoints to create a path.

### General rules of thumb:
1) Plan your path with generous amounts of checkpoints.
2) Give corners many extra checkpoints to make it appear smoother, rather than linear and rigid.
3) Remember to adjust the chance of failure, as well as fail positions along the checkpoints.
4) MAKE SURE YOU ARE MOVING THE CHECKPOINTS!!! NOT THE ROPE TRANSFORM POINTS!!!

In order for the rope to actually move, you have to call the StartRopePull() function in the Rope class.

#### Example of calling StartRopePull();
```c#
using UnityEngine;

public class Debug_PullRopeOnKeyPress : MonoBehaviour
{
    public Rope rope;

    private void Update()
    {
        if (rope != null)
        {
            if (Input.GetKeyDown(KeyCode.P))
            {
                rope.StartRopePull();
            }
        }
    }
}
```
## Rope.cs

### float ropePullSpeed
Speed the rope gets "pulled" at.

### Checkpoint[] checkpoints 
Array of all checkpoints for the "cable track".

### TransformPoint[] transformPoints
Array of all transform points of the rope

### int currentCheckpoint
Current checkpoint to move towards. This will update when the wire reaches the next checkpoint.

### CurvedLine2D curvedLine
Reference to the CurvedLine2D component.

### void StartRopePull()
Call this to activate the "pulling" of the rope / cable.

### void NextCheckpoint()
Increments the current checkpoint, then sets the next checkpoint on all transform points to the next

### TransformPoint[] GetTransformPoints()
Returns `transformPoints` as an array.

## Checkpoint.cs

### float failChance
Every checkpoint has a float value called `failChance`. This value represents the percent chance of a cable movement error while crossing the checkpoint. It should range from 0-1.

### Transform failPosition
`failPosition` is a reference to the transform of a failPosition object attatched to each checkpoint. If the checkpoint triggers a fail, the transformPoint of the wire that has the same index as the current checkpoint will adjust to the failPosition. The goal is for this to give it the effect of getting caught or veering out of place.

## TransformPoint.cs

### bool hasReachedCheckpoint
True if the transform point has reached its matching checkpoint

### bool isLastPoint
True if the last point on the cable. It should automatically be checked when generating a cable, but if it isn't you will get an error.

### bool canMove
True if the transform point can move.

### bool incremented
True if the NextCheckpoint method has been called, so it doesnt keep calling itself.

### int inded
This is used to point the transform point to its matching checkpoint.

### float speed
How fast the transform point will move to the next checkpoint. (assigned by `Rope.cs`)

    
    private float speed;                            //Speed of movement (does nothing right now
    private Checkpoint nextPoint;                   //Checkpoint being moved towards
    private Rope p_rope;                            //Parent object rope
    private Vector3 startPos;                       //Starting position of this object in world space
    private Vector3 adjustedPos;                    //Adjustment point if the checkpoint fails
    bool adjusting = false;                         //True if the checkpoint failed and the point is adjusting / moving to the adjustment point
