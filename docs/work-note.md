PHP：Foreach
---
可以很容易地通过在 $value 之前加上 & 来修改数组的元素。此方法将以引用赋值而不是拷贝一个值。
    
	<?php
	$arr = array(1, 2, 3, 4);
	foreach ($arr as &$value) {
	    $value = $value * 2;
	}
	// $arr is now array(2, 4, 6, 8)
	unset($value); // 最后取消掉引用
	?>