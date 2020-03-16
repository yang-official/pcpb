# PCPB

- write in markdown
- source control
- output to PDF, epub
- code syntax highlighting

## PDF
```
# pandoc version 2.7.3
mkdir -p build

pandoc \
    --pdf-engine=xelatex \
    --template=./templates/eisvogel.latex \
    --highlight-style tango \
    --toc -N \
    --filter pandoc-crossref \
    -o build/output.pdf \
    src/title.txt src/*.md
```
## epub
```
# pandoc version 2.7.3
mkdir -p build

pandoc \
    --filter pandoc-crossref \
    --css templates/epub.css \
    --toc -N \
    -o build/output.epub \
    src/title.txt src/*.md
    # -f markdown+smart -t markdown-smart \
```
