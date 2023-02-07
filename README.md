# html-to-gutenberg

## 1. Edit
- [ ] Find `(?<=<.+.>)(.*?)(?=<.*\/.+.?>)`
- [ ] Replace with `<RichText value={attributes.myRichText} default={"$1"} onChange={(newtext) => setAttributes({ myRichText: newtext })}/>`
- [ ] Find `\{attributes\.(.*?)\}`
- [ ] Select all occurrences (CMD + Shift + L)
- [ ] CMD + Shift + P -> Increment selection (requires an extension)
- [ ] Find  `default=\{"`
- [ ] Replace with `} default={"`
- [ ] Replace `\}\}` with `}`
- [ ] Find `\{attributes\.(.*?)\} default=\{"(.*?)"\} onChange=\{\(newtext\) => setAttributes\(\{ myRichText: newtext \}\)\}`
- [ ] Replace with `{attributes.$1} default={"$2"} onChange={(newtext) => setAttributes({ $1: newtext })}`

## 2. Attributes
- [ ] Find `\{attributes\.(.*?) default=\{"(.*?)"\}`
- [ ] Select all (CMD Shift + L)
- [ ] Paste in a draft file
- [ ] Find `\{attributes\.(.*?)\} default=\{"(.*?)"\}`
- [ ] replace with `"$1": {type: 'string', default: `$2`},`

## 3. Save
In a new file
- [ ] Find `default=\{"(.*?)"\} onChange=\{\(newtext\) => setAttributes\(\{ (.*?): newtext \}\)\}`
- [ ] replace with nothing
- [ ] Find `<RichText value=(.*?)/>`
- [ ] Replace with `<RichText.Content value=$1/>`
- [ ] replace `className=`with `class=`

## 4. Buttons

Buttons can have different structures other than Gutenberg's button block. Wherever RichText won't work:

Add this to your “href”
```{attributes.myRichText.match('(.*?)href\=\"(.*?)\"(.*?)') ? attributes.myRichText.match('(.*?)href\=\"(.*?)\"(.*?)')[2] : attributes.myRichText}```

Replace the labels with
```{attributes.myRichText.match('(?<=<.+.>)(.*?)(?=<.*\/.+.?>)') ? attributes.myRichText.match('(?<=<.+.>)(.*?)(?=<.*\/.+.?>)')[0] : attributes.myRichText} ```

## 5. Images

- [ ] Import the media upload block component.
- [ ] Find `<img src=“(.*?)” class=(.*?)>`
- [ ] Replace with:

```
imageUrl: {
  attribute: 'src',
  selector: 'img',
  default: $2
},

<MediaUpload onSelect={ media => { setAttributes({ imageUrl: media.url }); } } type="image" render={ ({ open }) => (<img src={ attributes.imageUrl} onClick={ open } className='$1'/>)}/>
```

Where

`ImageUrl`is a unique image attribute.

