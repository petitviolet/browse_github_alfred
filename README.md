# Alfred workflow to browse Github repository

## requirement

- ghq
- jq
- jo

## Usage

- Activate Alfred window
- Hit a commnad
    ```
    gh <query>
    ```
- Shows list of repositories that are placed in local by `ghq get`.
- Choose one of them
- Browse in Github

## script

Tiny script is used in this workflow.

```
export PATH="$HOME/go/bin:/usr/local/bin:$PATH"
i=0
items=$(for repo in $(ghq list | grep {query}); do
 let i++;
 jo uid="${i}" title="${repo}" subtitle="GitHub: ${repo}" arg="${repo}"
done | jo -a)

cat <<EOS
{
	"items": ${items}
}
EOS
```

## Licence

[MIT](https://petitviolet.mit-license.org)
