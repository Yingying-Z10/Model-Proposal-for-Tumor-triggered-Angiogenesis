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

 * _Type1: inhibitor that binds to VEGF, the most important factor released by tumor cells. This type of inhibitors acts as antibody which binds to VEGF and triggers immune response to remove VEGF. Angiogenesis will not be initiated without VEGF._

 * _Type2: inhibitor that directly interacts with endothelial cells and prevents their migration._ 

&nbsp; 


## Model Outline
****
&nbsp; 
### 1) Environment
_Description of the environment in your model. Things to specify *if they apply*:_
_The environment will be an area near a blood vessel within a human body. Initially, it will consist of an existing blood vessel at a fixed location. And as the simulation continues, the growth of new branches will be triggered by tumors:_
* _Boundary condition: infinite_
* _Dimensionality: 2D_
* _Environment-owned variables:_
  
   _location of the existing blood vessel, growth rate of new blood vessel branch_
* _Environment-owned methods/procedures:_

   _growth of new blood vessels from the existing ones_
  
   
   


```python
import math
import numpy
import random

g_rate=5 # growth rate of blood vessel

# Construct the blood vessel
Class BV(object):
  def __init__(self, x, y, g_rate):
    self.x=x
    self.y=y
    self.growth_rate=g_rate
    self.bound=False
    
  def branch_grow(self, VEGF_list, Inhibitor_list, bc_V, inhibitor_type, bc_I): 
    # bc_V & bc_I: binding coefficient of VEGF & inhibitor respectively
    growing=False
    near_VEGF_list=[]
    near_inhibitor_list=[]
    total_near_VEGF_distance=0
    total_near_inhibitor_distance=0
    
    # append all the VEGF that are close to the blood vessel cell into the list "near_VEGF_list"
    for VEGF in VEGF_list:
      #calculate the distance between a VEGF and the blood vessel cell
      distance=math.sqrt((VEGF.x-self.x)**2+(VEGF.y-self.y)**2)
      if distance<2: 
        total_near_VEGF_distance+=distance
        near_VEGF_list.append(VEGF)
        
    # for type 2 inhibitor, append all the inhibitors that are close to the blood vessel cell into the list "near_inhibitor_list"
    if inhibitor_type==2:
      for inhibitor in Inhibitor_list:
        #calculate the distance between an inhibitor and the blood vessel cell
        distance=math.sqrt((inhibitor.x-self.x)**2+(inhibitor.y-self.y)**2)
        if distance<2:
          total_near_inhibitor_distance+=distance
          near_inhibitor_list.append(inhibitor)
    
    # if the inhibitor is type 1, it does not interact with blood vessel cells. The blood vessel growth depends only on VEGF binding. If a VEGF is bound by an inhibitor, it will not be able to bind to the blood vessel cell
    if inhibitor_type==1 and bound==False:
      for VEGF in near_VEGF_list:
        if random.random()<bc_V and VEGF.attached=False:
          VEGF.attached=True
          growing=True
          bound==True
          break
          
      if growing==Ture:
        # the function "find_center_point" finds the geometric center of the group near the blood vessel and returns its location
        center_VEGF=find_center_point(near_VEGF_list)
        # grow the blood vessel
        BV_grow(center_VEGF)
     
    # if the inhibitor is type 2, it competes with VEGF in binding with blood vessel cells. If the average distance between the group of inhibitors is smaller than that of VEGF, the blood vessel will not grow. Otherwise, the blood vessel will grow 
    if inhibitor_type==2 and bound==False:
      if total_near_VEGF_distance/len(near_VEGF_list) < total_near_inhibitor_distance/len(near_inhibitor_list):
        growing=False
      else:
        growing=True
        bound=True
        
      if growing==True:
        center_VEGF=find_center_point(near_VEGF_list)
        BV_grow()
    
  def BV_grow(self, center):
    #calculate moving direction
    BV_location=point(self.x, self.y)  #location of the BV cell
    move_vector=unit_vector_from_2points(BV_location, center) # calculate the unit vector from the BV cell to the target center 
      
    # generating new blood vessel cells. The number of new BV cells depends on the growth rate
    for i in range(growth_rate):
      new_BV_x=int(self.x+i*move_vector[0])
      new_BV_y=int(self.x+i*move_vector[1])
      new_BV=BV(new_BV_x, new_BV_y, g_rate)
        
      # BV_list is the list that contains all the current blood vessel cells
      BV_list.append(new_BV)
    
        
# Create space and initial blood vessel at fixed location
space=numpy.zeros((grid_size, grid_size),dtype=numpy.int8)
for row in range(grid_size):
  for col in range(grid_size):
     # Determine if this cell will be a blood vessel cell
     if row==int(grid_size*0.8)
       cell_type = 1
     else:
       cell_type = 2
       
     # Set the space
     space[row, col] = cell_type
```

&nbsp; 

### 2) Agents
 
 _The agents in this model include 3 types of agents: tumor cells, VEGF released by tumor cells and inhibitors:_
 
* _Agent-owned variables:_

   _**Tumor**: tumor locations, tumor sizes, VEGF release rate_
   
   _**VEGF**: VEGF migration speed, VEGF binding coefficient_
   
   _**Inhibitor**: inhibitor migration speed, inhibitor binding coefficient_ 

* _Agent-owned methods/procedures:_

   _**Tumor**: tumor growth, release VEGF_
   
   _**VEGF**: move, bind to blood vessel, die_
   
   _**Inhibitor**:_ 
   
   * _Type 1: move, bind to VEGF, die_
   * _Type 2: move, bind to blood vessel, die_


```python

r_constant=30 # VEGF release rate of the tumor
V_speed=1.5 # migration speed of VEGF
I1_speed=1.8 # migration speed of type 1 inhibitor
I2_speed=2.0 # migration speed of type 2 inhibitor
V_dying_rate=0.5 # dying rate of VEGF
I1_dying_rate=0.4 # dying rate of type 1 inhibitor
I2_dying_rate=0.4 # dying rate of type 2 inhibitor

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

Class VEGF(object):
  def __init__(self, x, y, speed):
    self.x=x
    self.y=y
    self.speed=speed
    self.bound=false
    self.inactive=false
  
  # VEGF migration
  def moving(self):
    dx=self.speed*random.uniform(-1,1)
    dy=self.speed*random.uniform(-1,1)
    self.x+=dx
    self.y+=dy
  
  # VEGF dying: a while after it is bound to either type 1 inhibitor or the blood vessel, it will be removed from the system
  def dying(self):
    if self.bound==True:
      value=V_dying_rate*(t-Tbound) # t is the current time and Tbound is the time when VEGF is attached
      if value<=0 or moved-out-of-boundary:
        self.inactive=true
        
Class Type1_inhibitor(object):
  def __init__(self, x, y, speed):
    self.x=x
    self.y=y
    self.speed=speed
    self.bound=false
    self.inactive=false
    
  # type1 inhibitor migration
  def moving(self):
    dx=self.speed*random.uniform(-1,1)
    dy=self.speed*random.uniform(-1,1)
    self.x+=dx
    self.y+=dy 
  
  # type1 inhibitor binding to VEGF
  def binding(self):
    for VEGF in VEGF_list:
      distance=math.sqrt((self.x-VEGF.x)**2+(self.y-VEGF.y)**2)
      if distance<2:
        self.bound=True
        VEGF.bound=True
  
  # type1 inhibitor dying: a while after it is bound to VEGF, it will be removed from the system
  def dying(self):
    if self.bound==True:
      value=I1_dying_rate*(t-Tbound) # t is the current time and Tbound is the time when inhibitor is attached
      if value<=0 or moved-out-of-boundary:
        self.inactive=true
        
Class Type2_inhibitor(object):
  def __init__(self, x, y, speed):
    self.x=x
    self.y=y
    self.speed=speed
    self.inactive=false
    
  # type2 inhibitor migration
  def moving(self):
    dx=self.speed*random.uniform(-1,1)
    dy=self.speed*random.uniform(-1,1)
    self.x+=dx
    self.y+=dy 
  
  # type2 inhibitor dying: a while after it enters the system, it will be removed from the system
  def dying(self):
    if moved-out-of-boundary:
      self.inactive=true


# This may be a set of "turtle-own" variables and a command in the "setup" procedure, a list, an array, or Class constructor
# Feel free to include any agent methods/procedures you have so far. Filling in with pseudocode is ok! 
```

&nbsp; 

### 3) Action and Interaction 
 
**_Interaction Topology_**

_Type 1 inhibitor:_
* _VEGF interacts with inhibitors through spatial proximity_
* _blood vessels interact with VEGF through spatial proximity_ 

_Type 2 inhibitor:_
* _inhibitors interact with blood vessels through spatial proximity_
* _VEGF interacts with blood vessels through spatial proximity_
 
**_Action Sequence_**

1. _Tumor cells release VEGF._
2. _VEGF dissipates in the environment. The movement of VEGF will be against its gradient, meaning that the less amount of VEGF the region has, the more likely a particle of VEGF will move there._
3. _VEGF triggers blood vessel growth when it moves to a location that is within a pre-defined radius of a blood vessel._
4. _Inhibitors enter the system. The model for type 1 inhibitor and that for type 2 inhibitor will be different:_

   _Type 1 inhibitor: Inhibitors interact with VEGF. When the distance between an inhibitor and a VEGF is within a pre-defined threshold, the VEGF will be removed from the system after a pre-defined amount of time._

   _Type 2 inhibitor: Inhibitors interact with blood vessels through spatial proximity and compete with VEGF. Within a pre-defined radius, if the averaged distance of the inhibitors near the blood vessel cell is smaller than that of the VEGFs near the same blood vessel cell, no new blood vessel cell will grow from it._

&nbsp; 
### 4) Model Parameters and Initialization

_global parameters:_

* _grid size_
* _time_
* _blood_vessel_cell_list
* _VEGF_list_
* _tumor_cell_list_
* _type1_inhibitor_list_
* _type2_inhibitor_list_


_Describe how your model will be initialized_
_

_Provide a high level, step-by-step description of your schedule during each "tick" of the model_

&nbsp; 

### 5) Assessment and Outcome Measures

_The results will be measured using the following parameters:

* _change in tumor cell size (Change_TuSize = Tumor_Size(final)-Tumor_Size(initial))_
* _time (t)_
* _inhibitor concentration (inh_c = number-of-inhibitors/simulation-area)_

_The effectiveness of the inhibitors will be measured using the formula **(Change_TuSize/t)/inh_c**, indicating the growth rate of the tumor cell at the given amount of inhibitors. The smaller the result, the more effective the inhibitor is.

&nbsp; 

### 6) Parameter Sweep

_What parameters are you most interested in sweeping through? What value ranges do you expect to look at for your analysis?_
_I'm interested in sweeping through the types of the inhibitors and the concentrations of the inhibitors._ 
