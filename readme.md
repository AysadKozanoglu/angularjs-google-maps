# AngularJS Google Maps

AngularJS library for working with Google Maps

## Places Autocomplete directive

The `gmPlacesAutocomplete` directive turns an input into an input that listens for user input and provides place predictions based on the input:

    <input type="text" gm-places-autocomplete="options" ng-model="modelName" />
    
- *options*: optional, options you wish to pass to the [`google.maps.places.Autocomplete`](https://developers.google.com/maps/documentation/javascript/reference?hl=nl#Autocomplete) service. See the [`AutocompleteOptions` specifications](https://developers.google.com/maps/documentation/javascript/reference?hl=nl#AutocompleteOptions) for a [complete list of available options](https://developers.google.com/maps/documentation/javascript/reference?hl=nl#AutocompleteOptions).
- *modelName*: optional, name of the model you wish to assign the resulting object to
    
As soon as the user selects a place, the following happens:

- the `ngModel` is assigned an object with the following properties:
  + *element*: the current element
  + *api*: provides access to the [`google.maps.places.Autocomplete`](https://developers.google.com/maps/documentation/javascript/reference?hl=nl#Autocomplete) service
- a `gmPlacesAutocomplete::placeChanged` event is broadcasted

Example controller:

    angular.module('places', ['gm'])
        .controller('placesAutocompleteCtrl', ['$scope', function($scope){
      
            // Define options
            $scope.options = {};
            
            // Listen to change event
            $scope.$on('gmPlacesAutocomplete::placeChanged', function(){
              console.log('Place changed');
              console.dir(arguments);
            });
  
        }]);
      
The model provides access to the [`google.maps.places.Autocomplete`](https://developers.google.com/maps/documentation/javascript/reference?hl=nl#Autocomplete) service API so you can do things like:

    // Listen to change event
    $scope.$on('gmPlacesAutocomplete::placeChanged', function(){
      
        // Get place
        console.dir(modelName.api.getPlace());
        
        // Get bounds
        console.dir(modelName.api.getBounds());
      
    });
    
    
Check out the [Autocomplete documentation](https://developers.google.com/maps/documentation/javascript/reference?hl=nl#Autocomplete) for a [complete list of available methods](https://developers.google.com/maps/documentation/javascript/reference?hl=nl#Autocomplete).

## Change log

### 0.1.0

- Added gmPlacesAutocomplete directive

### 0.2.0

- Added logger service
- Updated gmPlacesAutocomplete directive to use logger service

