## txtmng

Automatically manage variables in your configs and more.

txtmng takes `file`, checks if template for it exists exists, does sed replace operations based on specified rules on the template it and saves result into `file`

The main benefit of txtmng is ability to configure equivalent stuff (like colors) in different programs in same place. Making for example changing themes much easier.

### Paths

#### config file

First check ./.txtmng (allowing for local edits (source the main config for overlay like system))

Then ${HOME}/.txtmng

Then ${HOME}/.txtmng.d/rules

main thing to look for is config associative array

```bash
config=(
	[template-dir]="$HOME/.txtmng.d/templates" #specifies location for templates array
)
```

then there's rules associative array, [word-to-replace-in-template]=with-what-it-should-be-replaced

#### templates

either define
```bash
files=(
   	path/relative/to/\$\{HOME\}/something.config
)
```

and it'll use
`path/relative/to/\$\{HOME\}/something.config.template`

as a template and 

`path/relative/to/\$\{HOME\}/something.config`

as a target

OR

```bash
templates=(
	[weird-thing.config]="${HOME}/PATH/to/A/thing.config"
)
```
and it'll use `~/.txtmng.d/templates/weird-thing.config` as a template and

`"${HOME}/PATH/to/A/thing.config"` as a target.

### Example

Terminal colors

#### alacritty.yml.template

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

#### ~/.txtmng.d/templates/XTerm-colors

```
*background: #!?background
*foreground: #!?foreground
*color0:  #!?black
*color8:  #!?bright-black
*color1:  #!?red
*color9:  #!?bright-red
*color2:  #!?green
*color10: #!?bright-green
*color3:  #!?yellow
*color11: #!?bright-yellow
*color4:  #!?blue
*color12: #!?bright-blue
*color5:  #!?magenta
*color13: #!?bright-magenta
*color6:  #!?cyan
*color14: #!?bright-cyan
*color7:  #!?white
*color15: #!?bright-white
```

#### .txtmng.d/rules

```bash
# txmng rule configuration

# to which files apply substitutions
# (we can assume being in homedir since ~ doesnt work here)

# take template from same dir as target
files=(
	.config/alacritty/alacritty.yml # template is alacritty.yml.template
)
# or from teplate dir
templates=(
	XTerm-colors="${HOME}/XTerm"
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
