# ARCGIS Integrations Introduction

ArcGIS provides a powerful set of tools for searching and displaying locations on a map.
 To generate map directions for a user when they search for a particular location using ArcGIS API for JavaScript in a React application,

1. Install the ArcGIS API for JavaScript uing npm.
        Run the following command in the terminal:
        'npm install@ arcgis/core'.

2. Import these required modules in the React component, from the ArcGIS API for JavaScript: 'Map', 'MapView','Directions'.

3. Create a new map.
        In the component's 'render' methodd, create a new 'Map' object from the '@arcgis/core/Map' module.

4. Add a directions widget. Add the 'Directions' widhet to the map using the '@arcgis/core/widgets/Directions' module.

5. Configure directions options.
       Configure 'DirectionsViewModel' object with the required options, such as the transprtation mode, start and end locations, and route styles.

6. Display directions
        Once the user has entered their start and end locations and submitted the search, he 'DirectionsViewModel'object will
        return a set of directions that the user can follow to get from one location to another. These directions can be displayed
        on the map using the 'Directions' widget.
Here is an example of how to use the ArcGIS API to generate map directions in React:

```javascript
import React,{Component} from "react";
import {loadModules} from "esri-loader";

class MapDirections extends Component{
    constructor(props){
        super(props);
        this.state = {
            directionsWidget: null,
            map: null
            view: null
        };
    }

    componentDidMount(){
        //load the required ArcGIS API modules
        loadModules([
            "esri/Map",
            "esri/views/MapView",
            "esri/widgets/Directions",
            "esri/widgets/Directions/DirectionsViewModel"
        ]).then(([Map, MapView, Directions, DirectionsViewModel])=> {
            //Create a new map object
            const map = newMap({
                basemap: "streets-navigation-vector"
            });
            //Create a new map view
            const view = new MapView({
                container: "viewDiv",
                map: map,
                center: [-118.2437, 34.0522],
                zoom: 12
            });
            //Create new  directions widget and add it to the view
            const directionsWidget = new Directions({
                view: view
            });
            view.ui.add(directionsWidget, {
                position: "top-right",
                index: 0
            });
            //Configure directions options
            const directionsViewModel = new DirectionsViewModel({
                view: view
            });
            directionsWidget.viewModel= directionsViewModel;
            directionsViewModel.mode= "driving";
            directionsViewModel.stops= new esri/Graphic({
                geometry: {
                    type: "point",
                    longitude: -117.1956,
                    latitude
                }
            });
        });
    };
};
