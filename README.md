# inherent_strain_simulation
This code was made to simulate inherent strain phenomena that appear during AM.


# How to use it ?
Inside the Normal config section change the path of the folder where the meshed file are (MSH file) and add the path where you want the result.

```python
'''
NORMAL CONFIG
'''

#We have here the path to the folder with the msh files and the path where we want the results:
dataset = '/meshed'
results_folder = '/results/'
```

You can chnage the boundary condition and add what you want:

```python
  # -------------------- #
  #   Create boundaries  #
  # -------------------- #
  
  class BoundaryBottom_func(SubDomain):
    def inside(self, x, on_boundary):
      #x[2] is z axe, fixing bottom surface. 
      # return on_boundary and near(x[2], 2., tol) #no fix bottom regarde si on peut pas mettre une petite distance
      return on_boundary and x[2] <= 0.0 #fix bottom surface / Before cutting / We fix everything that is 0< or =0
      #return on_boundary and x[0] <=10.0 and x[1] <= 12.0 #partie massive fixe
```

Same idea for the material. Go on the material section and chnge the mechanical properties of your material:
```python
  # ---------------- #
  #  Material param  #
  # ---------------- #

  #The material is : IN-718_powder 

  E = 191000  #Young's modulus (MPa) 
  nu = 0.31   #Poisson's ratio
```

Inside the class IS the IS parameters are found for a specific material and a specific BC.
Keep in mind that if you cnahe the mateial or the BC the IS parameters have to be chnaged.
For more information concerning the IS parametrs please refer the document called "IS parametrs"
```python
class InherentStrainFunc(UserExpression):
    def eval(self, value, x):

```


# References
https://github.com/floiseau/msh2xdmf
