
<!DOCTYPE html>
<html>
<style>
table, th , td  {
  border: 1px solid grey;
  border-collapse: collapse;
  padding: 5px;
}
table tr:nth-child(odd) {
  background-color: #f1f1f1;
}
table tr:nth-child(even) {
  background-color: #ffffff;
}
</style>
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.4.8/angular.min.js"></script>
<body>

<div ng-app="myApp" ng-controller="customersCtrl"> 

	<div class="container">
        <div class="row">
            <div class1="col-md-12">
                <div class="panel panel-default">
                    <div class="panel-body">
                        <form ng-submit="addNew()">
                            <table class="table table-striped table-bordered">
                                <thead>
                                    <tr>
                                        <th><input type="checkbox" ng-model="selectedAll" ng-click="checkAll()" /></th>
                                        <th>Firstname</th>
                                        <th>Lastname</th>
                                        <th>Email</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr ng-repeat="personalDetail in personalDetails">
                                        <td>
                                            <input type="checkbox" ng-model="personalDetail.selected"/></td>
                                        <td>
                                            <input type="text" class="form-control" ng-model="personalDetail.fname" required/></td>
                                        <td>
                                            <input type="text" class="form-control" ng-model="personalDetail.lname" required/></td>
                                        <td>
                                            <input type="email" class="form-control" ng-model="personalDetail.email" required/></td>
                                    </tr>
                                </tbody>
                            </table>

                            <div class="form-group">
                                <input ng-hide="!personalDetails.length" type="button" class="btn btn-danger pull-right" ng-click="remove()" value="Remove">
                                <input type="submit" class="btn btn-primary addnew pull-right" value="Add New">
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>


</div>

<script>
var app = angular.module('myApp', []);
app.controller('customersCtrl', function($scope) {

$scope.personalDetails = [
        {
            'fname':'abc',
            'lname':'l',
            'email':'abc@gmail.com'
        },
        {
            'fname':'jkl',
            'lname':'a',
            'email':'jkl@gmail.com'
        },
        {
            'fname':'lmn',
            'lname':'a',
            'email':'lmn@gmail.com'
        }];
		
		$scope.addNew = function(personalDetail){
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
     
});
</script>

</body>
</html>
