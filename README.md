# LadyBird-Web-Technical-Question

_**Q:Find substring of first inputstring which cover all second inputstring letters with minimum lenght?**_

```php
function findsubstring($input1,$input2)
{
    $results = array();
    $count = 0;
    for($i=0;$i<strlen($input2);$i++) {
        $temp = 0;
        for($j=0;$j<strlen($input1);$j++) {
            if($input2[$i] == $input1[$j])
            {
                if($temp == 0)
                {
                    $count++;
                }
                $temp++;
                $results[$i][]= $j;
            }
        }
    }
    $r = combinations($results);
    ksort($r);
    $return = reset($r);

    return substr($input1, min($return), max($return)-min($return)+1);
}

function combinations($arrays, $i = 0) {
    if (!isset($arrays[$i])) {
        return array();
    }
    if ($i == count($arrays) - 1) {
        return $arrays[$i];
    }

    $tmp = combinations($arrays, $i + 1);

    $result = array();

    foreach ($arrays[$i] as $v) {
        foreach ($tmp as $t) {
            if(is_array($t)){
                $r = array_merge(array($v), $t);
                $k = max($r)-min($r);
                $result[$k] = $r;
            } else {
                $r = array($v, $t);
                $k = max($r) - min($r);
                $result[$k] = $r;
            }
        }
    }
    return $result;
}

echo findsubstring("234506781230151341","305");
```
