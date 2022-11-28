# Qooper Parking System

## Get status of all parking lots
```GET``` ```127.0.0.1/lots```

```
{
    lots: [
        "A1": {
            floor: 1,
            available: true
        },
        "A2": {
            floor: 1,
            available: false,
            enterDate: 1669675666,
            licensePlate: "34AB123"
        }
        ...
    ],
}
```

## Get status of a parking lot
```GET``` ```127.0.0.1/lot/:lotName```

```
{
    lot: {
        "A1": {
            floor: 1,
            available: true
        }
    },
}
```

## Reserve a parking lot

### In there, we are caching data with lot name. So we can check it when we are trying to send a request. If data exists or not
### If data is not existing it means the lot is empty. Because we are deleting the data when a lot is gets empty.

```POST``` ```127.0.0.1/lot/:lotName```

### Request Body
```
{
    lot: "A1",
    licensePlate: "34AB123",
    enterDate: (Date.now() / 1000),

}
```
### Response
```
{
    "A1": {
        floor: 1,
        available: false,
        enterDate: 1669676122,
        licensePlate: "34AB123",
    },
}
```

### Failed Response
```
{
    error: {
        message: "A1 is already taken"
    }
}
```

## Exit and Calculate Fee
```DELETE``` ```127.0.0.1/lot/:lotName```

### Response
```
{
    lot: "A1",
    floor: 1,
    enterDate: 1669676122,
    exitDate: 1669676706,
    licensePlate: "34AB123"
    fee: 60,
}
```
