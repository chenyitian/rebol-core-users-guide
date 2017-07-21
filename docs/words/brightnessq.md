# Brightness? - Function Summary

## Summary:

Returns the monochrome brightness (0.0 to 1.0) for a color value.

## Usage:

**brightness? color**

## Arguments:

**color** - The color argument. (must be: tuple)

## Description:

This function converts an RGB tuple to a black and white brightness value between between 0 and 1.

```
print brightness? 255.255.255
1.0
```

```
print brightness? 0.0.0
0.0
```

```
print brightness? 255.0.0
0.27
print brightness? 128.128.128
0.501960784313725
```