**Description**
This task involves calculating the Forward Kinematics (FK) and Inverse Kinematics (IK) for a robotic arm with 3 Degrees of Freedom (DoF). The goal is to determine the position and orientation of the robot's end-effector based on the joint angles (FK) and to find the required joint angles to achieve a desired end-effector position (IK).

**Forward Kinematics (FK)**
Forward Kinematics involves determining the position and orientation of the robot's end-effector (usually a gripper or tool) based on the joint angles.

**Steps for FK:**
1. Define the Transformation Matrices for each Joint: Each joint's transformation matrix depends on its respective joint angle (θ_i) and link length (L_i).

      * For Joint 1:
        
      ![image](https://github.com/user-attachments/assets/061922bd-f6fe-42ae-9ca6-e7f8c60fcbd2)
      
      * For Joint 2:
      
      ![image](https://github.com/user-attachments/assets/c70028eb-e0f6-4c11-a2ea-093a7e4c4753)
      
      * For Joint 3:
        
      ![image](https://github.com/user-attachments/assets/b950acd5-4440-41d9-aed5-ce5dc1af84d8)

2. Compute the Overall Transformation Matrix: Combine the transformation matrices of all joints to get the overall transformation from the base to the end-effector.
 ```ruby
T = T_1 x T_2 x T_3
```
3. Extract the End-Effector Position: The position of the end-effector in the workspace can be obtained from the translation part of the final transformation matrix 𝑇.
```ruby
 [x,y,z] = [T_14, T_24, T_34]
```


************************************************************


**Inverse Kinematics (IK)**
Inverse Kinematics involves determining the joint angles (𝜃_1, 𝜃_2, 𝜃_3) that achieve a desired end-effector position.

**Steps for IK:**
 Specify the Desired End-Effector Position: Choose the desired position (𝑥_𝑑, 𝑦_d, 𝑧_𝑑) in the workspace where you want the end-effector to move.
     
1. Calculate 𝜃_1:

![image](https://github.com/user-attachments/assets/43832691-f834-4e24-83da-3d52f58a16c9)

2. Calculate 𝑟 and 𝐷: First, calculate 𝑟:

![image](https://github.com/user-attachments/assets/b1a15ada-85ba-4eed-a478-0b1f2ece0900)

Then, calculate 𝐷:

![image](https://github.com/user-attachments/assets/f5ac3719-a866-4ad1-8ecb-b07336c99540)


3. Calculate θ_2:

![image](https://github.com/user-attachments/assets/95183054-8677-4c47-8aa0-610b29987b0a)


4. Calculate θ_3:

![image](https://github.com/user-attachments/assets/54b76b69-8fdc-4aa7-9ef8-b445306a73d9)


**Example Calculation:**
* Assume 𝐿_1 = 2, L2 = 2, 𝐿_3 = 1
* Desired end-effector position (x_d, y_d, z_d) = (3,3,0).

     1. Calculate θ_1:
        
     ![image](https://github.com/user-attachments/assets/25ebe478-9a42-4d26-819f-cee43256100a)
     
     
     2. Calculate 𝑟:
     
     ![image](https://github.com/user-attachments/assets/8c74abd9-711f-4677-93de-51dffe721ac9)
     
     3. Calculate 𝐷:
     
     ![image](https://github.com/user-attachments/assets/b4d47e76-5bf9-43f3-9ca9-1e527c9a5fd7)
     
     4. Calculate θ_2:
        
     ![image](https://github.com/user-attachments/assets/0af28014-7cf4-4a96-8c7c-3da414cd5611)
     
     
     5. Calculate θ_3:
     
     ![image](https://github.com/user-attachments/assets/f34e17f9-7db7-42b5-8fab-4d8708975d74)

```ruby
θ_3 ≈ arctan2 (−2,4.24) − 30.96 − 45 ≈ −18.43 degrees
```
These calculated angles 𝜃_1 ≈ 45, θ_2 ≈ 30.96, and 𝜃_3 ≈ −18.43 degrees would position the end-effector at the desired coordinates.
