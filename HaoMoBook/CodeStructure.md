# 页面代码结构

## 列表页

```angular2html
vm.setSearchParams  = function(resetFlag){
      var deferred = $q.deferred();

      $q.all([1, 2]).then(function(values){
        vm.search.filters = {
          'table': {
            'column': {
              'in': values[0]
            }
          }
        }
      }, function(err){

      });

      Restangular().then(function(res){
        deferred.resolve(res.data);
      }, function(err){
        deferred.reject();
      });

      return deferred.promise;
    };

    vm.search = function(){
      vm.setFilters().then(function(data){
        vm.process(data);
      }, function(err){
        console.log(err);
      });

      Restangular().then(function(res){
        vm.process(data);
      })
    };

    vm.process = function(data){

    };
```

## 编辑页

```angular2html
vm.item = {};

    vm.loadItem = function(id){
      Restangular().then(function(res){
        vm.item = res.data;
      })
    };

    vm.clearBeforeUpdate = function(){

    };

    vm.updateItem = function(){
      vm.clearBeforeUpdate();
      Restangular().post()
    };

    vm.columnOnChange = function(value){

    };
```