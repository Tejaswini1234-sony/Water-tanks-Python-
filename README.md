# Water-tanks-Python-
**Problem Statement-** > To find the cubic meters of water that can be poured into the series of tanks before the water level reaches the top of tank1 

**Code:**

```
from math import sqrt

n = int(input("Enter number of tanks: "))

#Array for height of each tank
list = []
for i in range(0,n):
    height = float(input("Enter height of tank "+str(i+1)+": "))
    list.append(height)

#Array for height of connecting pipe from ground     
list1 = []
for i in range(0,n-1):
    height_cp = float(input("Enter height of connecting pipe "+str(i+1)+": "))
    list1.append(height_cp)

input("Enter Zero : ")  
    
#volume of open tank
crosssectional_area = 1
volume_opentank = crosssectional_area * list[0]

#pressure by air
#p1v1 = p2v2
#excess pressure in air = pressure applied by water

vol = []
vol.append(volume_opentank)

#volume of closed tanks
def volume_closedtank(list,list1,vol):
    for i in range(0,n-1):
    #p[i] = list1[i] / list[i+1]-h
        a  = 0.097
        b  = -(0.097*list[i+1])-(0.097*list[i])-1
        c = 0.097*list[i]*list[i+1]+list[i+1]-list1[i]
        d = (b**2)-(4*a*c)

        if d > 0:
         sol1 = (((-b)+sqrt(d))/(2*a))
         sol2 = (((-b)-sqrt(d))/(2*a))
        elif d == 0:
         sol1 = (-b) / 2*a
         vol.append(sol1)
        else:
         print("no roots")
        
        if sol1 <= list[i+1]:
          vol.append(sol1)
        else:
          vol.append(sol2)
    return vol

#finding sum of volumes in all tanks
def find_volume(vol):
    total = 0
    for ele in range(0,len(vol)):
       total = total +vol[ele]
       total_vol = float("{0:.3f}".format(total))
    return total_vol

volume_closedtank(list, list1, vol)
print("volume of all tanks:",find_volume(vol))

```

**Sample Input**
Enter number of tanks: 2

Enter height of tank 1: 10

Enter height of tank 2: 8

Enter height of connecting pipe 1: 4

Enter Zero : 0

**Sample Output**
volume of all tanks: 15.26
