# Model Proposal for Tumor-triggered Angiogenesis
_Yingying Zeng_
* Course ID: CMPLYXSYS 530
* Course Title: Computer Modeling of Complex System
* Term: Winter 2018

&nbsp; 

### Goal 
*****
 
_The goal of my model is to simulate the angiogenesis process triggered by tumors. The simulations will include different inhibitors and test their effects on reducing angiogenesis and therefore preventing tumors from growing._

&nbsp;  
### Justification
****
_The process of tumor-triggered angiogenesis is a complex system involving different agents such as tumor cells and endothelial cells. The growth of blood vessels is a result from interactions between the proteins released by the tumor cells and the receptors on the endothelial cells. Using ABM, I can predict the formation of new blood vessels; and by adding inhibitors to the systems, I can test whether certain inhibitor can prevent the tumor cells from growing and compare the efficiencies of different inhibitors._

&nbsp; 
### Main Micro-level Processes and Macro-level Dynamics of Interest
****

_The key process I am interested in exploring is how the inhibitors interact with either the proteins released by the tumor cells or the endothelial cells to prevent the blood vessels from reaching the tumor cells, and therefore preventing tumor growth. I will test 2 types of inhibitors and compare their effects._
* inhibitor that binds to VEGF, the most important factor released by tumor cells. This type of inhibitors acts as antibody which binds to VEGF and triggers immune response to remove VEGF. Angiogenesis will not be initiated without VEGF.
* inhibitor that directly interacts with endothelial cells and prevents their migration. 

&nbsp; 


## Model Outline
****
&nbsp; 
### 1) Environment
_Description of the environment in your model. Things to specify *if they apply*:_

* _Boundary conditions (e.g. wrapping, infinite, etc.)_
* _Dimensionality (e.g. 1D, 2D, etc.)_
* _List of environment-owned variables (e.g. resources, states, roughness)_
* _List of environment-owned methods/procedures (e.g. resource production, state change, etc.)_


```python
# Include first pass of the code you are thinking of using to construct your environment
# This may be a set of "patches-own" variables and a command in the "setup" procedure, a list, an array, or Class constructor
# Feel free to include any patch methods/procedures you have. Filling in with pseudocode is ok! 
# NOTE: If using Netlogo, remove "python" from the markdown at the top of this section to get a generic code block
```

&nbsp; 

### 2) Agents
 
 _Description of the "agents" in the system. Things to specify *if they apply*:_
 
* _List of agent-owned variables (e.g. age, heading, ID, etc.)_
* _List of agent-owned methods/procedures (e.g. move, consume, reproduce, die, etc.)_


```python
# Include first pass of the code you are thinking of using to construct your agents
# This may be a set of "turtle-own" variables and a command in the "setup" procedure, a list, an array, or Class constructor
# Feel free to include any agent methods/procedures you have so far. Filling in with pseudocode is ok! 
# NOTE: If using Netlogo, remove "python" from the markdown at the top of this section to get a generic code block
```

&nbsp; 

### 3) Action and Interaction 
 
**_Interaction Topology_**

_Description of the topology of who interacts with whom in the system. Perfectly mixed? Spatial proximity? Along a network? CA neighborhood?_
 
**_Action Sequence_**

_What does an agent, cell, etc. do on a given turn? Provide a step-by-step description of what happens on a given turn for each part of your model_

1. Step 1
2. Step 2
3. Etc...

&nbsp; 
### 4) Model Parameters and Initialization

_Describe and list any global parameters you will be applying in your model._

_Describe how your model will be initialized_

_Provide a high level, step-by-step description of your schedule during each "tick" of the model_

&nbsp; 

### 5) Assessment and Outcome Measures

_What quantitative metrics and/or qualitative features will you use to assess your model outcomes?_

&nbsp; 

### 6) Parameter Sweep

_What parameters are you most interested in sweeping through? What value ranges do you expect to look at for your analysis?_
