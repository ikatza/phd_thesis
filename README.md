# phd_thesis

To build use:


```
latexmk phdthesis
```


The contents of my `~/.latexmkrc`

```
$pdf_previewer = 'open -a Skim';
$pdflatex = 'lualatex -file-line-error -synctex=1 %O %S';
$biber='biber --validate-datamodel %O %S';
$pdflatex = 'lualatex -file-line-error -synctex=1 %O %S && ln -fs %D %R.pdf';
$out_dir = 'auto';
$pdf_mode = 1;

add_cus_dep( 'acn', 'acr', 0, 'makeglossaries' );
add_cus_dep( 'glo', 'gls', 0, 'makeglossaries' );
$clean_ext .= " acr acn alg glo gls glg";
sub makeglossaries {
  my ($base_name, $path) = fileparse( $_[0] );
  pushd $path;
  my $return = system "makeglossaries", $base_name;
  popd;
  return $return;
}

```
