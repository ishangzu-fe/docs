# 知租侠接口

### 字典接口

1.所有字典

```javascript
  var url = SERVER.url + '/DictController/getDictList.action';
    var obj = {
      keys:'Gender,CustomerFrom,RentClass,RentType,Education,RentUse,CustomerInvalidType,CustomerStatus,SearchRoomType,CustomerListType,CustomerRentPriceOrderType,HouseRoomFeature,Orientation,FireStatus,FitmentType,HouseSizeSearchType,ApartmentListSortType,RentStatus,EntrustType,CustomerViewReason,CustomerViewResult,SpiderPaymentCycle,SpiderPaymentCycleBankloans,ApartmentTaxesBears,SignBody,SpiderPromotion,CardType,ApartmentContractFeeType,SpiderRentUse,NewApartmentContractPaymentType'
    }

    return $post(url,obj);
```

2.商圈字典

```javascript
var url = SERVER.url + '/CommController/sercherBudinessCircle.action';
    return $get(url,null);
```



### 自营房源

1.房源列表

```javascript
 var url = SERVER.url + '/HouseController/selectApartmentList.action';

var obj = {
        pageNumber: $scope.currentPage,
        pageSize: 10,
        rent_type: $scope.rentTypeIndex,
        area_code_search: $scope.area_code_search,
        business_circle_search: $scope.business_circle_search,
        rent_price: $scope.rentPanelIndex,//租金
        rooms: $scope.searchRoomsIndex,
        house_room_feature_ids: $scope.HouseRoomFeatureIndex,
        rent_status: $scope.RentStatusIndex,
        fire_status: $scope.FireStatusIndex,
        fitment_type: $scope.FitmentTypeIndex,
        orientation: $scope.OrientationIndex,
        build_area: $scope.HouseSizeSearchTypeIndex,
        sort: $scope.orderIndex,
        formType: $scope.houseType,

        apartment_id: House.searchHouseModel.apartment_id,
        building_id: House.searchHouseModel.building_id,
        residential_id: House.searchHouseModel.residential_id
      }
    return $post(url,obj);
```

2.整租房源详情接口

```javascript
 var url = SERVER.url + '/HouseController/selectApartmentDetail.action';

var obj = {
    apartment_id: $stateParams.apartment_id + ""
  };
    return $post(url,obj);
```

3.合租房源详情接口

```javascript
 var url = SERVER.url + '/HouseController/selectShareHouseDetail.action';

var obj = {
    apartment_id: $stateParams.apartment_id + ""
  };
    return $post(url,obj);
```

4.根据经纬度获取可带看小区信息

```javascript
 var url = SERVER.url + '/HouseController/getResidentialInfoForMap.action';

var obj = {
          latitude: lat.toString(),
          longitude: lng.toString(),
          radius: "0.5"
        }

    return $post(url,obj);
```

5.根据小区信息获取可带看的房源列表

```javascript
 var obj = {
      residentialId:data.id,
      pageNumber:1,
      pageSize:1000
    }
      var url = SERVER.url + '/HouseController/searchByResidentialId.action';
    return $get(url,obj);
```

6.开锁接口

```javascript
var url = SERVER.url + '/HouseController/openLock.action';

    return $post(url,obj);
```

7.房源搜索

```javascript
var obj = {
      search: $scope.inputVal,
      pageNumber: $scope.currentPage,
      pageSize: 10,
      formType: $stateParams.formType
    };
```

