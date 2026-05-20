# Q&A

This chapter lists common problems with using myBlockly to control robotic arms for reference.

**Q1: When running myBlockly, an error message `ModuleNotFoundError: No module named 'pymycobot'`**

A: This is caused by not installing the pymycobot library when setting up the Python environment. To install the pymycobot library, you need to open the terminal (Win key + R key), enter: `pip install pymycobot --upgrade --user`, and click the Enter key to see Successfully installed pymycobot.

<img src="../../../resources/5-BasicApplication/5.2/5.2.1/img/Q&A/pymycobotinstallation.jpg" style="zoom: 50%;" />

**Q2: The robot arm is unresponsive because the `sleep` method module is not added**

A: The program to operate the robot arm takes time to complete, so after an action, a `sleep' module needs to be connected to give the robot arm time to move before proceeding with the next movement (the time required depends on the situation, the machine The default setting of the arm is to run myBlockly with a minimum sleep time of no less than 0.5s), otherwise the robotic arm will not be able to achieve the ideal movement.

**Q3: The `Run` button in the upper right corner cannot be clicked and is gray-green. **

A: The new version of myBlockly adds the function of detecting the serial communication of the robot arm. If the robot arm is currently connected to the computer, you need to check:

(1) Whether there is a background program occupying the serial port of the robotic arm;

(2) Whether the toolbar under the red arrow on the right is closed. If it is open, it needs to be closed manually.

**Q4: Why doesn't the machine respond after running the program?**

A: Please confirm if the port number selection is correct, `/dev/ttyACOM0`. If the port is correct but there is still no response, please contact the after-sales service.

**Q5: The result of running the program shows child process exited with code 1**
A: This is not an error. All programs return the binary number 1 after running. It means everything has been successfully run.

---

 [← Previous Page](./4-ioTest.md) | [Next Page →](../5.2.2-mystudio/README.md)
