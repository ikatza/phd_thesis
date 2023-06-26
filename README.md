# phd_thesis

To build use:


```
latexmk phdthesis
```

latexmk: https://mg.readthedocs.io/latexmk.html


Skim to inspect the pdf: https://skim-app.sourceforge.io




The contents of my `~/.latexmkrc`

```
$pdf_previewer = 'open -a Skim';
$pdflatex = 'lualatex -interaction=batchmode  -draftmode -no-pdf -file-line-error -synctex=1 -output-driver="xdvipdfmx -z0" %O %S';
$pdflatex = 'lualatex -interaction=nonstopmode -file-line-error -synctex=1 -output-driver="xdvipdfmx -z3" %O %S && ln -fs %D %R.pdf';
$biber='biber --validate-datamodel %O %S';
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


Every now and then biber becomes corrupted, or something. I find that
the best is to delete the cache, clear previous compilation, and then
recompile like normal. To clear the old stuff I do:


``` shell
 rm -fr `biber --cache` && rm -r auto/
```
