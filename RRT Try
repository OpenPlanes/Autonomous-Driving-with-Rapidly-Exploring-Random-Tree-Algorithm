import networkx as nx
import matplotlib.pyplot as plt
from matplotlib.patches import Rectangle
from random import randrange
import numpy as np
import math
from math import sqrt
from networkx.classes.function import path_weight

def rrt(World,Start,End,Obs,Res):
	nodes = {}
	nodes[0] = (Start[0],Start[1])
	nodePoses = []
	nodePoses.append(Start)
	tree = nx.Graph()
	pathFound = False
	minLen = float("inf")
	itr = 0
	while pathFound == False:
		newNode = [randrange(0,World[0]),randrange(0,World[1])]
		minid = float("inf")
		
		closest = -1
		for i in range(len(nodePoses)):
			if np.hypot(nodePoses[i][0]-newNode[0],nodePoses[i][1]-newNode[1]) <= Res:
				if np.hypot(nodePoses[i][0]-newNode[0],nodePoses[i][1]-newNode[1]) <= minid:
					minid = np.hypot(nodePoses[i][0]-newNode[0],nodePoses[i][1]-newNode[1])
					closest = i
				else:
					pass
			else:
				pass
		if closest != -1:
			for k in range(len(Obs)):
				centDist = collisionCheck(newNode,nodePoses[closest],[Obs[k][0],Obs[k][1]])
				if centDist<= Obs[k][2]:
					closest = -1
				else:
					pass
		if closest != -1:
			itr+=1
			nodePoses.append(newNode)
			nodes[itr] = (newNode[0],newNode[1])
			tree.add_edge(closest,itr,weight=np.hypot(nodePoses[closest][0]-nodePoses[itr][0],nodePoses[closest][1]-nodePoses[itr][1]))
			if np.hypot(End[0]-newNode[0],End[1]-newNode[1]) <=  End[2]:
				if nx.shortest_path_length(tree,source=0,target=itr,weight='weight') <= minLen:
					pathFound=True
				else:
					pass
			else:
				pass
		else:
			pass
		
	options = {
		"font_size": 1,
		"node_size": 3,
		"node_color": "white",
		"edgecolors": "green",
		"linewidths": 5,
		"width": 5,
	}
	path = nx.shortest_path(tree,0,itr,weight='weight')
	nx.draw_networkx(tree, nodes, **options)
	path_x = []
	path_y = []
	for j in range(len(path)):
		path_x.append(nodePoses[path[j]][0])
		path_y.append(nodePoses[path[j]][1])
	
	plt.plot(path_x,path_y)
	endRegion =plt.Circle((End[0],End[1]),End[2],color='r')

	ax = plt.gca()
	for l in range(len(Obs)):
		ax.add_patch(plt.Circle((Obs[l][0],Obs[l][1]),Obs[l][2],color='y'))
	ax.add_patch(endRegion)
	plt.axis("on")
	plt.show()

def collisionCheck(A,B,E):
 	#From https://www.geeksforgeeks.org/minimum-distance-from-a-point-to-the-line-segment-using-vectors/?ref=lbp
    # vector AB
    AB = [None, None];
    AB[0] = B[0] - A[0];
    AB[1] = B[1] - A[1];
 
    # vector BP
    BE = [None, None];
    BE[0] = E[0] - B[0];
    BE[1] = E[1] - B[1];
 
    # vector AP
    AE = [None, None];
    AE[0] = E[0] - A[0];
    AE[1] = E[1] - A[1];
 
    # Variables to store dot product
 
    # Calculating the dot product
    AB_BE = AB[0] * BE[0] + AB[1] * BE[1];
    AB_AE = AB[0] * AE[0] + AB[1] * AE[1];
 
    # Minimum distance from
    # point E to the line segment
    reqAns = 0;
 
    # Case 1
    if (AB_BE > 0) :
 
        # Finding the magnitude
        y = E[1] - B[1];
        x = E[0] - B[0];
        reqAns = sqrt(x * x + y * y);
 
    # Case 2
    elif (AB_AE < 0) :
        y = E[1] - A[1];
        x = E[0] - A[0];
        reqAns = sqrt(x * x + y * y);
 
    # Case 3
    else:
 
        # Finding the perpendicular distance
        x1 = AB[0];
        y1 = AB[1];
        x2 = AE[0];
        y2 = AE[1];
        mod = sqrt(x1 * x1 + y1 * y1);
        if mod != 0:
        	reqAns = abs(x1 * y2 - y1 * x2) / mod
        else:
        	reqAns=0
    return reqAns;



def main():
	World = [50,50] #Map size
	Start = [1,1] #Start coordinate
	End = [30,30,1] #End Coordinate with radius
	Obs = [[20,15,2.5],[20,12.5,2.5],[20,10,2.5],[20,7.5,2.5],[20,5,2.5],[10,20,3],[7,20,3],[4,20,3],[1,20,3],[20,18,3],[20,21,3],[20,24,3],[20,27,3],[20,30,3]] #Obstacles and obstacle radii
	Res = 7 #Resolution of rrt
	rrt(World,Start,End,Obs,Res)

if __name__ == '__main__':
	main()
