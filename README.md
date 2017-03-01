
<!DOCTYPE html>
<html ng-app="myApp">

<head>

<style>
table, th , td  {
  border: 1px solid grey;
  border-collapse: collapse;
  padding: 5px;
}

.text-center{
	text-align: center
}
</style>

<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css">

<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.4.8/angular.min.js"></script>

</head>
<body>
<div ng-controller="myCtrl">
<h2 class="text-center">Simple table app</h2>


<div class="container">
<div class="row">
<div class="col-md-12">
<form ng-submit="addNew()">
		
	Search:
	<span style="padding: 5px;">
	<input type="text" class="form-control ng-valid ng-dirty" ng-model="searchKeyword">
	</span>
		
	<table class="table">
		<thead>
			<tr>
				<th><input type="checkbox" ng-model="selectedAll" ng-click="checkAll()" /></th>
				<th>Firstname</th>
				<th>Lastname</th>
				<th>Email</th>
			</tr>
		</thead>
		<tbody>
			<tr ng-repeat="personalDetail in personalDetails | filter: searchKeyword">
				<td>
					<input type="checkbox" ng-model="personalDetail.selected"/>
				</td>
				<td>
					<input type="text" class="form-control" ng-model="personalDetail.fname" required/>
				</td>
				<td>
					<input type="text" class="form-control" ng-model="personalDetail.lname" required/>
				</td>
				<td>
					<input type="email" class="form-control" ng-model="personalDetail.email" required/>
				</td>
			</tr>
		</tbody>
	</table>
	
	<div class="form-group">
		<input ng-hide="!personalDetails.length" type="button" class="btn btn-danger pull-right" ng-click="remove()" 			value="Remove">
		<input type="submit" class="btn btn-primary addnew pull-right" value="Add New">
	</div>
</form>
</div>
</div>
</div>
</div>
<script>
var app = angular.module("myApp", []);
app.controller("myCtrl",['$scope', function($scope){

console.log('entrede my contrl');

$scope.personalDetails = [
        {
            'fname':'Muhammed',
            'lname':'Shanid',
            'email':'shanid@shanid.com'
        },
        {
            'fname':'John',
            'lname':'Abraham',
            'email':'john@john.com'
        },
        {
            'fname':'Roy',
            'lname':'Mathew',
            'email':'roy@roy.com'
        }];
		
	$scope.addNew = function(){
            $scope.personalDetails.push({ 
                'fname': "", 
                'lname': "",
                'email': "",
            });
        };
		
	$scope.remove = function(){
            var newDataList=[];
            $scope.selectedAll = false;
            angular.forEach($scope.personalDetails, function(selected){
		 if(!selected.selected){
                    newDataList.push(selected);
                }
            });
			
            $scope.personalDetails = newDataList;
        };
		
	$scope.checkAll = function () {
		if (!$scope.selectedAll) {
			$scope.selectedAll = true;
		} else {
			$scope.selectedAll = false;
		}
		angular.forEach($scope.personalDetails, function(personalDetail) {			
			personalDetail.selected = $scope.selectedAll;				
		});
    };  

}]);

</script>
</body>
</html>
