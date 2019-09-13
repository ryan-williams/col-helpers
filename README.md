# col-helpers
bash helpers related to slicing/formatting columns from lines of text

## Install
```bash
git clone git@github.com:ryan-williams/col-helpers.git
echo "source $PWD/col-helpers/.cols-rc" >> ~/.bashrc
. ~/.bashrc
```

## Usage

### `col`: get columns or column-ranges from input
Write some test data:
```bash
cat <<EOF >foo
0 1 2 3 4 5 6
 0 1 2 3 4 5 6
00  11  22  33  44  55  66
00,11,22,33,44,55,66
EOF
```

Get columns from index 2 on:
```bash
cat foo | col 2:
# 2 3 4 5 6
# 2 3 4 5 6
# 22 33 44 55 66
# 
```

Get columns [2,4):
```bash
cat foo | col 2:4
# 2 3
# 2 3
# 22 33
# 
```

Negative indices work:
```bash
cat foo | col -2:
# 5 6
# 5 6
# 55 66
# 00,11,22,33,44,55,66
cat foo | col :-2
# 0 1 2 3 4
# 0 1 2 3 4
# 00 11 22 33 44
# 
cat foo | col 2:-2
# 2 3 4
# 2 3 4
# 22 33 44
# 
```

Slice an individual column:
```bash
cat foo | col -2
# 5
# 5
# 55
# 
```

Customize input/output delimiters:
```bash
cat foo | col -i, -o'|' 2:5
# 
# 
# 
# 22|33|44
```

Multiple columns/ranges can be separated by commas:
```bash
cat foo | col 1,3:-1
# 1 3 4 5
# 1 3 4 5
# 11 33 44 55
# 
```

### `first`, `second`, `last`
shorthands for `col 0`, `col 1`, and `col -1`, resp.

### `splt`: split N-column lines into N lines each
```bash
echo 1 2 3 4 5 | spc
# 1
# 2
# 3
# 4
# 5
echo 1,2,3,4,5 | sp,
# 1
# 2
# 3
# 4
# 5
```

See alias definitions in [`.cols-rc`](./.cols-rc).
### `column -t` aliases
Align columns by a given delimiter.

Write some test data:
```bash
cat <<EOF>foo
a,b,c,d,e
AAAAA,BBBBB,CCCCC,DDDDD,EEEEE
111,222,333,444,555
EOF
```

Format:
```bash
ct, foo
# a      b      c      d      e
# AAAAA  BBBBB  CCCCC  DDDDD  EEEEE
# 111    222    333    444    555
```

See alias definitions in [`.cols-rc`](./.cols-rc).
