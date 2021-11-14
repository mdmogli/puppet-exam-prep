# Loops

[INDEX](../../README.md)

## each: iterate values from an array, hash or any iterable object.
```python
$binaries = ['facter', 'hiera', 'mco', 'puppet', 'puppetserver']

$binaries.each |String $binary| {
  file {"/usr/bin/${binary}":
    ensure => link,
    target => "/opt/puppetlabs/bin/${binary}",
  }
}
```

## slice: Slices an array or hash into pieces of a given size.
```python
$a.slice(2) |$entry|          { notice "first ${$entry[0]}, second ${$entry[1]}" }
$a.slice(2) |$first, $second| { notice "first ${first}, second ${second}" }

slice([1,2,3,4,5,6], 2) # produces [[1,2], [3,4], [5,6]]
slice(Integer[1,6], 2)  # produces [[1,2], [3,4], [5,6]]
slice(4,2)              # produces [[0,1], [2,3]]
slice('hello',2)        # produces [[h, e], [l, l], [o]]
}
```
## filter: removes non-matching elements
```python
# For the array $data, return an array containing the values that end with "berry"
$data = ["orange", "blueberry", "raspberry"]
$filtered_data = $data.filter |$items| { $items =~ /berry$/ }
# $filtered_data = [blueberry, raspberry]
```

## map: apply a function to every value and returns the result
```python
# For the array $data, return an array containing each value multiplied by 10
$data = [1,2,3]
$transformed_data = $data.map |$items| { $items * 10 }
# $transformed_data contains [10,20,30]

# For the hash $data, return an array containing the keys
$data = {'a'=>1,'b'=>2,'c'=>3}
$transformed_data = $data.map |$items| { $items[0] }
# $transformed_data contains ['a','b','c']
```

## reduce: apply a function to every value saving result in every iteration:
memo is mandatory as a varible and it saves the last iteration value

```python
# Reduce the array $data, returning the sum of all values in the array.
$data = [1, 2, 3]
$sum = $data.reduce |$memo, $value| { $memo + $value }
# $sum contains 6
```
