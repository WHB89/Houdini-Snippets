'''
Create new geo nodes by material 
'''
import hou
previous_selection = hou.selectedNodes()
valuesList = []
node = hou.pwd()
nodePath = previous_selection[0].path()

currentOutputNode = hou.node('/obj/BuildingA_1/building/OUT_WALL_GEO')
hou_parent = hou.node("/obj/BuildingA_1")
# Fill List
for prim in previous_selection[0].geometry().prims() :
    value = prim.attribValue("shop_materialpath")
    valueAlreadyExists = False
    if(len(str(value)) < 1):
        value = "noMaterialAssigned"
    for i in range(0,len(valuesList)):
        if(str(valuesList[i]) == str(value)):
            valueAlreadyExists = True
    
    if(valueAlreadyExists == False):
        valuesList.append(str(value))
        
        
print valuesList
    #materialName = value.split('/')
#str(materialName[len(materialName)-1])

for valueType in range(0,len(valuesList)):
    print valuesList[valueType]
    nameArray = str(valuesList[valueType]).split('/')
    materialName = str(nameArray[len(nameArray)-1])
    thisGeo = hou_parent.createNode("geo", materialName)
    thisMergeNode = thisGeo.createNode("object_merge", "object_merge")
    nodeLink = thisMergeNode.parm("objpath1")
    nodeLink.set(str(nodePath))
    thisDeleteNode = thisGeo.createNode("delete", "delete")
    thisDeleteNode.setInput(0, thisMergeNode)
    thisDeleteNode.setDisplayFlag(True)
    thisDeleteNode.setRenderFlag(True)
    deleteOperation = thisDeleteNode.parm("negate")
    deleteOperation.set(1)
    deleteGeoType = thisDeleteNode.parm("entity")
    deleteGeoType.set(0)
    deleteType = thisDeleteNode.parm("groupop")
    deleteType.set(2)
    deleteExpression = thisDeleteNode.parm("filter")
    if(str(valuesList[valueType]) != "noMaterialAssigned"):
        expression = 'strmatch(@shop_materialpath, "'+ str(valuesList[valueType])+'")'
    else:
        expression = 'strmatch(@shop_materialpath, "")'
    deleteExpression.setExpression(expression) 
    
'''
Create new geo nodes by point attribute
'''

import hou
previous_selection = hou.selectedNodes()
valuesList = []
node = hou.pwd()
nodePath = previous_selection[0].path()

currentOutputNode = hou.node('/obj/BuildingA_1/building/OUT_WALL_GEO')
hou_parent = hou.node("/obj/BuildingA_1")
# Fill List
for point in previous_selection[0].geometry().points() :
    value = point.attribValue("name")
    valueAlreadyExists = False
    for i in range(0,len(valuesList)):
        if(str(valuesList[i]) == str(value)):
            valueAlreadyExists = True
    if(valueAlreadyExists == False):
        valuesList.append(str(value))
        
        
print valuesList

for valueType in range(0,len(valuesList)):
    print valuesList[valueType]
    thisGeo = hou_parent.createNode("geo", str(valuesList[valueType]))
    thisMergeNode = thisGeo.createNode("object_merge", "object_merge")
    nodeLink = thisMergeNode.parm("objpath1")
    nodeLink.set(str(nodePath))
    thisDeleteNode = thisGeo.createNode("delete", "delete")
    thisDeleteNode.setInput(0, thisMergeNode)
    deleteOperation = thisDeleteNode.parm("negate")
    deleteOperation.set(1)
    deleteGeoType = thisDeleteNode.parm("entity")
    deleteGeoType.set(1)
    deleteType = thisDeleteNode.parm("groupop")
    deleteType.set(2)
    deleteExpression = thisDeleteNode.parm("filter")
    expression = 'strmatch(@name, "'+ str(valuesList[valueType])+'")'
    deleteExpression.setExpression(expression) 
    

