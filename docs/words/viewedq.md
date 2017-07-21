# Viewed? - Function Summary

## Summary:

Returns TRUE if face is displayed.

## Usage:

**viewed? face**

## Arguments:

**face** - The face argument. (must be: object)

## Description:

This function provides an easy way to determine if a face is currently shown.

```
out-face: layout [
	h2 "Testing"
]
print viewed? out-face
false
```

```
view/new out-face
print viewed? out-face
true
```

```
unview
```

Note that if the face is off-screen or minimized this function will still return TRUE.

## Related:

[**view**](http://www.rebol.com/docs/words/wview.html) - Displays a window face.