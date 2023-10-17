# Replace string in file

```js
const replaceStringInFile = (filePath, search, replace) => {

const lines = fs.readFileSync(filePath, 'utf8').split(/\r?\n/);

const newLines = lines.map((line) => line.replace(search, replace));

fs.writeFileSync(filePath, newLines.join('\n'), 'utf8');

};
```

#node #javascript 