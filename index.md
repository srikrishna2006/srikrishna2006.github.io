# Advanced Robotics Programming

This course will cover the two essential tools that every robotics programmer must have; PID Control and Odometry Tracking System. Usually, beginner programmers are taught inaccurate methods for autonomous movement. It is usually believes that PID and Odometry are unreachable for beginners. However, I believe these concepts can be taught to anyone as long as they are willing to learn. This is an easy, introductory course to quickly grasp and implement these concepts. With these two tools, any programmer can soar to the top and help their team compete for awards in competitions.

### PID

PID explanation

```markdown

void PID(double setpoint, double kP, double kI, double kD)
{
  double left = Left.position(turns);
  double right = Right.position(turns);
  double wheelDiameter = 3.25;
  double ave = (left + right)/2;
  double dist = ave * M_PI * wheelDiameter;
  double error = setpoint - dist;
  double prevError = error;
  double totalError = error;
  double derivative = 0;
  double integral = 0;
  double vel  = 0;
  while (error > 0.1 ) //  threshold value
  {
    derivative = error - prevError;
    integral = totalError;
    vel = kP * error + kI * integral + kD * derivative;
    LB.spin(forward,vel,percent);
    RB.spin(reverse,vel,percent);
    LF.spin(forward,vel,percent);
    RF.spin(reverse,vel,percent);
    left = Left.position(turns);
    right = Right.position(turns);
    ave = (left + right)/2;
    dist = ave * M_PI * wheelDiameter;
    error = setpoint - dist;
    prevError = error;
    totalError += error;


  }

}


```


### Odometry

Follow this [paper]([file:///Users/srikrishnagurumurthy/Library/CloudStorage/OneDrive-Personal/Odometry%20doc%2010J%20pdf.pdf](https://1drv.ms/b/s!AiHKcueme-JJzy-z3qbXo53DuXLg?e=AqjiaQ)) that I wrote to to understand the odometry process

```markdown
static double left_turns = 0.0;
static double right_turns = 0.0;
static double theta = 0.0;
static double x = 0.0;
static double y = 0.0;

//printf("Static %f %f %f %f, %f\n", left_turns, right_turns, theta, x, y);

// Get the turns from the encoder
double dleft = Left.position(turns);
double dright = Right.position(turns);

// Get the number of turns in the current cycle
// which is equal to current turns - previous turns
dleft -= left_turns;
dright -= right_turns;

// Store the total number of turns so far 
left_turns += dleft;
right_turns += dright;

// Use the formula to calculate the left and the right distance
// and the delta theta
double leftDist = dleft * PI * WHDIA;
double rightDist = dright * PI * WHDIA;
double dtheta = (leftDist - rightDist)/(2*RW);


// update the theta with delta theta and 
// fix the upper and lower bound


// Calculate distance and dx, dy
double dist = (rightDist + leftDist)/2;
double dy = dist * cos(theta + dtheta/2);
double dx = dist * sin(theta + dtheta/2);

// Update the robot x, y value with deltaX, deltaY
x += dx;
y += dy;

theta +=dtheta;
if (theta > 2*PI)
{
  theta -= (2*PI);
}
if (theta < -(2*PI))
{
  theta += (2*PI);
}
```


For more details see [Basic writing and formatting syntax](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/srikrishna2006/srikrishna2006.github.io/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
