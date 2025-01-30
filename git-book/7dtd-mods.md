# 7DTD mods

{% hint style="info" %}
This page refers to 7DTD alpha 21
{% endhint %}

## General

### Modlets vs mods

## Files structure

```
7dtdInstallDir
 + Mods
    + TheMod
       + Config/
          + Localization.txt
          + <XMLfiles>
          + XUi/
       + Resources/
       + UIAtlases/ItemIconAtlas/
       + ModInfo.xml
```

### ModInfo.xml

```xml
<xml>
    <Name value="MoreDoors" />
    <Description value="Adds more doors to craft" />
    <Author value="Pedru" />
    <Version value="1.0" />
</xml>
```

`Name` must respect the regex `^[0-9a-zA-Z_I-]+$`

### Localization.txt

Here the name of the items as they appear in the crafting menus must be listed, the first field must match the value of the `Name` field in `Blocks.xml`

{% code fullWidth="false" %}
```csv
Key,Source,Context,Changes,English,French,German,Klingon,Spanish
houseFrontDoor1_v1,blocks,Door,,Front Door,,Eingangstür,,Puerta
houseFrontDoor2_v1,blocks,Door,,Front Door,,Eingangstür,,Puerta
```
{% endcode %}

## XML files in `Config`

### Blocks.xml

{% code fullWidth="true" %}
```xml
<block name="BoxTruckhostess_b">
	<property name="Material" value="Mmetal"/>
	<property name="IsTerrainDecoration" value="false"/>
	<property name="Shape" vaalue="ModelEntity"/>
	<property name="Path" value="solid"/>
	<property name="Model" value="#@modfolder:Resources/BoxTruck.unity3d?BoxTruckhostess_b"/><property name="ModelOffset" value="0,0,0"/>
	<property name="Place" value="TowardsPlacerInverted"/>			
	<property name="OnlySimpleRotations" value="false"/>
	<property name="MultiBlockDim" value="1,1,1"/>
	<property name="Collide" value="movement,melee,bullet,arrow,rocket"/>	
	<property name="CustomIcon" value="BoxTruckhostess" />
	<property name="Stabilitysupport" value="false"/>
	<property name="CanPickup" value="false"/>
	<property name="MaxDamage" value="350"/>
	<property name="CreativeMode" value="Dev"/>
	<property name="Stacknumber" value="5"/>
	<property name="EconomicValue" value="1000"/>
	<property class="RepairItems"> <property name="resourceForgedIron" value="1"/> </property>			
	<property name="FilterTags" value="fdecor"/>
	<property name="SortOrder1" value="70a0"/>	
</block>
```
{% endcode %}

## Links

### 7DTD

* [Console commands](https://7daystodie.fandom.com/wiki/Command_Console)

### Basic mod doc

* [Basic modding tutorial](https://7daystodie.fandom.com/wiki/Basic_Modding_Tutorial_1)
* [Mod interface](https://7daystodie.fandom.com/wiki/Mod_Interface)
* [Mod structure](https://7daystodie.fandom.com/wiki/Mod_Structure)

### Advanced mods

* [ModAPI](https://7daystodie.fandom.com/wiki/ModAPI)

### XML files

* [XPath explained](https://7daystodie.fandom.com/wiki/XPath_Explained)
* [XML files](https://7daystodie.fandom.com/wiki/XML_Files)

### Mods source code

* [OCB mods source code repo](https://github.com/OCB7D2D)
* [Max Fox' source code](https://gitlab.com/maxfox_gaming)

### Youtube

* [Adding Recipes with XPath - 7 Days to Die XML Modding Tutorial for Beginners](https://www.youtube.com/watch?v=-GOjiyAaPS0\&list=PLfY-5aBkL7v_AAtm1TWEyKhAYb5RI828p)
* [Add arrows](https://www.youtube.com/watch?v=R-vAm54Vvro)
