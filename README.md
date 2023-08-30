## txtmng

Automatically manage variables in your configs and more.

txtmng takes `file`, checks if `file`.template exists, does sed replace operations on the template it and saves result into `file`

The main benefit of txtmng is ability to configure equivalent stuff (like colors) in different programs in same place. Making for example changing themes much easier.

### Example

Terminal colors

#### alacritty.yml

```yaml
colors:
  primary:
    background: '#!?background'
    foreground: '#!?foreground'

  normal:
    black:   '#!?black'
    red:     '#!?red'
    green:   '#!?green'
    yellow:  '#!?yellow'
    blue:    '#!?blue'
    magenta: '#!?magenta'
    cyan:    '#!?cyan'
    white:   '#!?white'

  bright:
    black:   '#!?bright-black'
    red:     '#!?bright-red'
    green:   '#!?bright-green'
    yellow:  '#!?bright-yellow'
    blue:    '#!?bright-blue'
    magenta: '#!?bright-magenta'
    cyan:    '#!?bright-cyan'
    white:   '#!?bright-white'
```

#### XTerm

```
*background: #000000
*foreground: #cccccc
*color0:  #101010
*color8:  #222222
*color1:  #bb2040
*color9:  #ff4066
*color2:  #338066
*color10: #55aa80
*color3:  #cc8844
*color11: #ffcc88
*color4:  #6655aa
*color12: #8070dd
*color5:  #bb55bb
*color13: #dd77dd
*color6:  #447099
*color14: #66aaaa
*color7:  #808080
*color15: #ffffff
```

#### .txtmng-rules

```bash
# txmng rule configuration

# to which files apply substitutions
# (we can assume being in homedir since ~ doesnt work here)

files=(
	.config/alacritty/alacritty.yml
	XTerm
)

# what to replace
# it's recomended to have some sort of prefix to avoid replacing words which
# should not have been replaced.

rules=(
	[!?background]='000000'
	[!?foreground]='cccccc'
	
	[!?black]='101010'
	[!?red]='bb2040'
	[!?green]='338066'
	[!?yellow]='cc8844'
	[!?blue]='6655aa'
	[!?magenta]='bb55bb'
	[!?cyan]='447099'
	[!?white]='808080'
	[!?bright-black]='222222'
	[!?bright-red]='ff4066'
	[!?bright-green]='55aa80'
	[!?bright-yellow]='ffcc88'
	[!?bright-blue]='8070dd'
	[!?bright-magenta]='dd77dd'
	[!?bright-cyan]='66aaaa'
	[!?bright-white]='ffffff'
)
```
