# PULLED ROPE GENERATOR 

###### NORCAT || Brandon Cotesta || Version 0.1.1

This tool was designed to make the process of generating pulled cable along a cable tray easier.
While it does generate all the necessary gameobjects, you still need to manually move the checkpoints to create a path.

###General rules of thumb:
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
##Checkpoints
