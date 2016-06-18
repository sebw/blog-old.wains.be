# bash

#### integer increment

	#!/bin/bash
	 
	x=1
	echo $x
	 
	(( x++ ))
	echo $x
	 
	(( x += 1 ))
	echo $x
	 
	let x++
	echo $x