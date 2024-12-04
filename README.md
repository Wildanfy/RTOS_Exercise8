# RTOS-EXERCISE 8
https://github.com/user-attachments/assets/fa053e5f-6690-4a58-8052-65a77cf9e9a1

# STM32 FreeRTOS LED Control Project

## Description
This project demonstrates a multi-threaded application running on an STM32 microcontroller using FreeRTOS. The application controls multiple LEDs connected to GPIO pins, with each LED being managed by a dedicated FreeRTOS task. The tasks demonstrate critical section handling to access shared resources safely.

## Features
- **FreeRTOS Integration:** The project leverages FreeRTOS for multi-threaded operations.
- **Multi-LED Control:** Each LED is controlled by a separate task with independent blink rates.
- **Critical Section Handling:** Proper handling of shared resources using FreeRTOS semaphore APIs.
- **Simulated Shared Resource Access:** Includes a simulated read-write operation on shared data.

## Project Structure
The key components of this project include:
- **Tasks:**
  - `GreenLedTask`: Controls the green LED (GPIOA Pin 0) with a 200ms delay.
  - `RedLedTask`: Controls the red LED (GPIOA Pin 1) with a 550ms delay.
  - `OrangeLedTask`: Toggles the orange LED (GPIOA Pin 3) every 50ms.
- **Shared Resource:** A `startFlag` variable, used to simulate shared data access.
- **Semaphore for Resource Management:** FreeRTOS semaphore (`CriticalResourceSemaphore`) ensures proper synchronization between tasks.

## Hardware Requirements
1. **STM32 Microcontroller**: Compatible with STM32CubeIDE (tested on STM32F401VGT6).
2. **LEDs**: At least three LEDs connected to GPIOA pins (Pin 0, Pin 1, Pin 3).
3. **Power Supply**: Provide adequate power for the STM32 board and peripherals.

## Software Requirements
1. **STM32CubeIDE**: Used for development and debugging.
2. **FreeRTOS**: Integrated as part of the STM32Cube HAL library.
3. **CMSIS-RTOS API**: For FreeRTOS task and kernel management.

## How It Works
1. **Initialization**:
   - HAL library initializes peripherals.
   - FreeRTOS kernel starts, and tasks are created.

2. **Task Functions**:
   - Each task toggles or sets its associated LED based on a fixed delay.
   - Tasks use a semaphore to access shared data (`startFlag`).

3. **Critical Section with Semaphore**:
   - Tasks use `osSemaphoreWait` and `osSemaphoreRelease` to ensure safe access to the shared resource.

## Configuration
### GPIO
- Configure GPIO pins for LEDs:
  - Green LED: GPIOA Pin 0
  - Red LED: GPIOA Pin 1
  - Orange LED: GPIOA Pin 3

### FreeRTOS Tasks
- Modify task definitions in `main.c` if additional LEDs or functionalities are required.

## Code Snippets
### Task Creation
```c
osThreadDef(HijauLedTask, GreenLedTask, osPriorityNormal, 0, 128);
HijauLedTaskHandle = osThreadCreate(osThread(HijauLedTask), NULL);
```

### Semaphore Usage Example
```c
osSemaphoreWait(CriticalResourceSemaphoreHandle, WaitTimeMilliseconds);
accessSharedData();
osSemaphoreRelease(CriticalResourceSemaphoreHandle);
```

### Simulated Shared Data Access
```c
void accessSharedData(void) {
    if (startFlag == 1) {
        startFlag = 0;
    } else {
        HAL_GPIO_WritePin(GPIOA, GPIO_PIN_2, GPIO_PIN_SET);
    }
    HAL_Delay(1000);
    startFlag = 1;
    HAL_GPIO_WritePin(GPIOA, GPIO_PIN_2, GPIO_PIN_RESET);
}
```

## Usage
1. Clone this repository to your local machine.
2. Open the project in STM32CubeIDE.
3. Compile and flash the code onto your STM32 microcontroller.
4. Observe the LEDs blinking based on the specified task logic.


## IOC Pin
https://github.com/user-attachments/assets/f8ec3eeb-e419-4fdf-9b1c-f1cd5ee2ceb0



## Demo Video
https://github.com/user-attachments/assets/ff9c19ef-236b-4189-9f1d-cb50e63f63e7
### Contributor
- Wildan Faizin (3222600011)
- Dhanang Fadhila Trisnandi (3222600015)
