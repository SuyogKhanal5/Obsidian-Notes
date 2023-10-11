- ### What is a computer?
	- ###### Main Components:
		- **CPU** - Central Processing Unit
		- **Memory** - Short Term Storage, gone after computer is turned off
		- **Bus** - Communication Channels between components
		- **I/O Devices** - Input/Output
			- **Human Interface** - Screen, Keyboard, Mouse, etc.
			- **Storage** - Stuff computer remembers even after it is turned off
			- **Networking** - Internet connections
			- **Graphics** - Display
		- Diagram: ![[Pasted image 20231009135415.png]]

- ### Von Neumann Model
	- Instead of making a specific computer to solve a specific problem, why not store instructions and data in memory
	- This would allow one computer to be used to solve multiple problems
	- Prior to this, computers would have to be rewired to solve a different problem ![[Pasted image 20231009135709.png]]

- ### Basic CPU Function
	- CPU will fetch, decode, and execute
	- Loops and Functions rely on this ![[Pasted image 20231009135748.png]]

- ### Running on Hardware
	- Machine Language is closest to the system, High-Level Language is converted to Assembly language and then converted to machine language ![[Pasted image 20231009135822.png]]

- ### Input/Output
	- Modification of Von Neumann Model for more modern use![[Pasted image 20231009135924.png]]![[Pasted image 20231009135933.png]]

- ### Operating Systems
	- Programs run on the hardware, calling into the OS for some services
	- ###### On modern systems, OS and hardware collaborate for some features
		- Ex. Virtual Memory, Multitasking
	- ###### Computers these days are designed to be used on an operating system
		- Many things that would be assumed to be done by the hardware, are now actually done by the Operating System
		- Partnership between OS and Hardware

- ### Computer Architecture
	- How to build components
	- How to design and build systems using components
	- How components are wired and how they communicate with one another

- ### Moore's Law
	- Gordon More was an Intel Engineer
	- ###### Observed that the number of transistors on a chip doubles every 18 months
		- Processor Speed doubles every 18 months
		- Memory capacity doubles every two years
		- Disk capacity doubles every year
	- Transistors on a chip (logarithmic scale)![[Pasted image 20231009140150.png]]
	- Clock Speed ![[Pasted image 20231009140158.png]]
	- CPU Performance ![[Pasted image 20231009140208.png]]
	- Memory Capacity ![[Pasted image 20231009140219.png]]
	- Disk Capacity ![[Pasted image 20231009140226.png]]
	- CPU-Memory Performance Gap (Why Caches were invented)![[Pasted image 20231009140250.png]]
	- Power Wall (Computers were running so hot that the CPU would melt, solution was multicore CPUs) ![[Pasted image 20231009140335.png]]

- ### Summary
	- Modern Systems are complex
	- Single Threaded programs run mostly the same as they did 20 years ago
	- Faster Processors and new systems enable new applications