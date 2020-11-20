# distanceLongitudeLatitudePhp
calculate distance between 2 points using latitude and longitude with php 



function distance($lat1, $lon1, $lat2, $lon2){
        $R = 6371; // km
        $dLat = toRad($lat2-$lat1);
        $dLon = toRad($lon2-$lon1);
        $lat1 = toRad($lat1);
        $lat2 = toRad($lat2);

        $a = sin($dLat/2) * sin($dLat/2) +sin($dLon/2) * sin($dLon/2) * cos($lat1) * cos($lat2); 
        $c = 2 * atan2(sqrt($a), sqrt(1-$a)); 
        $d = $R * $c;
        return $d;
}

// Converts numeric degrees to radians
function toRad($Value) 
{
    return $Value * pi() / 180;
}


# with sql 
SELECT latitude, longitude, SQRT(
    POW(69.1 * (latitude - [startlat]), 2) +
    POW(69.1 * ([startlng] - longitude) * COS(latitude / 57.3), 2)) AS distance
FROM TableName HAVING distance < 25 ORDER BY distance;

# with laravel  distance between 2 persons
$users = DB::table('users')
          ->select(DB::raw('name,SQRT(POW(69.1 * (latitude - 24.900110), 2) + POW(69.1 * (67.099760 -longitude) * COS(latitude / 57.3), 2)) AS distance'))
          ->havingRaw('distance < 25')
          ->OrderBy('distance')
          ->get();
