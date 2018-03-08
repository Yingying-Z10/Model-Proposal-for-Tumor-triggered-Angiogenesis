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
_The process of tumor-triggered angiogenesis is a complex system involving different agents such as proteins released by tumor cells and endothelial cells. The growth of blood vessels is a result from interactions between the proteins released by the tumor cells and the receptors on the endothelial cells. Using ABM, I can predict the formation of new blood vessels; and by adding inhibitors to the systems, I can test whether certain inhibitor can prevent the tumor cells from growing and compare the efficiencies of different inhibitors._

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
_The environment will be an area near a blood vessel within a human body and it will consist of tumor cells and the main blood vessel at fixed locations:_
* _Boundary condition: infinite_
* _Dimensionality: 2D_
* _environment-owned variables:_

   main blood vessel location
* _environment-owned methods/procedures (e.g. resource production, state change, etc.)_
  
   
   


```python

  
# This may be a set of "patches-own" variables and a command in the "setup" procedure, a list, an array, or Class constructor
# Feel free to include any patch methods/procedures you have. Filling in with pseudocode is ok! 
```

&nbsp; 

### 2) Agents
 
 _The agents in this model include 3 types of agents: tumor cells, VEGF released by tumor cells and inhibitors:_
 
* _Agent-owned variables:_

   **_Tumor_**: _tumor locations, tumor sizes, VEGF release rate
   
   **_VEGF_**:_VEGF migrating speed, VEGF binding coefficient
   
   **_Inhibitor_**: inhibitor migrating speed, inhibitor binding coefficient 

* _Agent-owned methods/procedures (e.g. move, consume, reproduce, die, etc.)_

   **_Tumor_**: _tumor growth, release VEGF
   
   **_VEGF_**: _move, bind to blood vessel, die
   
   **_Inhibitor_**: 
   
   * _Type 1: move, bind to VEGF, die
   * _Type 2: move, bind to blood vessel, die


```python
# Include first pass of the code you are thinking of using to construct your agents
# Construct the tumor cells:
Class Tumor(object):
  def __init__(self, x, y, radius, r_constant):
    self.x=x
    self.y=y
    self.radius=radius
    self.release_rate=r_constant*(radius**2)
     
  # tumor growth rate
  def tumor_growth_rate(self, grow=False, distance, g_constant)
    if grow==Ture:
      #growth rate of a tumor cell is inversely proportional to its distance to the main blood vessel 
      g_rate=g_constant/distance
      return g_rate
  
  # tumor growing
  def grow(self, tumor_growth_rate, grow=False):
    if grow==True:
      self.radius=tumor_growth_rate*self.radius
      
Tumor_num=3
for i in range(Tumor_num):
  x=


# This may be a set of "turtle-own" variables and a command in the "setup" procedure, a list, an array, or Class constructor
# Feel free to include any agent methods/procedures you have so far. Filling in with pseudocode is ok! 
# NOTE: If using Netlogo, remove "python" from the markdown at the top of this section to get a generic code block
```

&nbsp; 

### 3) Action and Interaction 
 
**_Interaction Topology_**

_Type 1 inhibitor:_
* VEGF interacts with inhibitors through spatial proximity
* endothelial cells interact with VEGF through spatial proximity 

_Type 2 inhibitor:_
* inhibitors interacts with endothelial cells through spatial proximity
* VEGF interacts with endothelial cells through spatial proximity
 
**_Action Sequence_**

1. Tumor cells release VEGF.
2. VEGF dissipates in the environment. The movement of VEGF will be against its gradient, meaning that the less amount of VEGF the region has, the more likely a particle of VEGF will move there. 
3. VEGF triggers endothelial cell migration when it moves to a location that is within a pre-defined radius of an endothelial cell.
4. Inhibitors enter the system. The model for type 1 inhibitor and that for type 2 inhibitor will be different:

   Type 1 inhibitor: Inhibitors interact with VEGF. When the distance between an inhibitor and a VEGF is within a pre-defined threshold, the VEGF will be removed after a pre-defined amount of time.

   Type 2 inhibitor: Inhibitors interact with endothelial cells through spatial proximity and compete with VEGF. Within a pre-defined radius, if the ratio of the inhibitor concentration over the VEGF concentration is above the pre-defined threshold, the endothelial cell will stop migrating.

&nbsp; 
### 4) Model Parameters and Initialization

_Describe and list any global parameters you will be applying in your model._

_Describe how your model will be initialized_

_Provide a high level, step-by-step description of your schedule during each "tick" of the model_

&nbsp; 

### 5) Assessment and Outcome Measures

* _change in tumor cell size (Change_TuSize = Tumor_Size(final)-Tumor_Size(initial))_
* _time (t)_
* _inhibitor concentration (inh_c)_

_The effectiveness of the inhibitors will be measured using the formula **(Change_TuSize/t)/inh_c**, indicating the growth rate of the tumor cell given inh_c mol/L inhibitor. The smaller the result, the more effective the inhibitor is.

&nbsp; 

### 6) Parameter Sweep

_What parameters are you most interested in sweeping through? What value ranges do you expect to look at for your analysis?_
_I'm interested in sweeping through the types of the inhibitors and the concentrations of the inhibitors._ 
