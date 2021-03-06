cola Report for recount2:ERP005938
==================

**Date**: 2019-12-25 22:26:22 CET, **cola version**: 1.3.2

----------------------------------------------------------------

<style type='text/css'>

body, td, th {
   font-family: Arial,Helvetica,sans-serif;
   background-color: white;
   font-size: 13px;
  max-width: 800px;
  margin: auto;
  margin-left:210px;
  padding: 0px 10px 0px 10px;
  border-left: 1px solid #EEEEEE;
  line-height: 150%;
}

tt, code, pre {
   font-family: 'DejaVu Sans Mono', 'Droid Sans Mono', 'Lucida Console', Consolas, Monaco, 

monospace;
}

h1 {
   font-size:2.2em;
}

h2 {
   font-size:1.8em;
}

h3 {
   font-size:1.4em;
}

h4 {
   font-size:1.0em;
}

h5 {
   font-size:0.9em;
}

h6 {
   font-size:0.8em;
}

a {
  text-decoration: none;
  color: #0366d6;
}

a:hover {
  text-decoration: underline;
}

a:visited {
   color: #0366d6;
}

pre, img {
  max-width: 100%;
}
pre {
  overflow-x: auto;
}
pre code {
   display: block; padding: 0.5em;
}

code {
  font-size: 92%;
  border: 1px solid #ccc;
}

code[class] {
  background-color: #F8F8F8;
}

table, td, th {
  border: 1px solid #ccc;
}

blockquote {
   color:#666666;
   margin:0;
   padding-left: 1em;
   border-left: 0.5em #EEE solid;
}

hr {
   height: 0px;
   border-bottom: none;
   border-top-width: thin;
   border-top-style: dotted;
   border-top-color: #999999;
}

@media print {
   * {
      background: transparent !important;
      color: black !important;
      filter:none !important;
      -ms-filter: none !important;
   }

   body {
      font-size:12pt;
      max-width:100%;
   }

   a, a:visited {
      text-decoration: underline;
   }

   hr {
      visibility: hidden;
      page-break-before: always;
   }

   pre, blockquote {
      padding-right: 1em;
      page-break-inside: avoid;
   }

   tr, img {
      page-break-inside: avoid;
   }

   img {
      max-width: 100% !important;
   }

   @page :left {
      margin: 15mm 20mm 15mm 10mm;
   }

   @page :right {
      margin: 15mm 10mm 15mm 20mm;
   }

   p, h2, h3 {
      orphans: 3; widows: 3;
   }

   h2, h3 {
      page-break-after: avoid;
   }
}
</style>




## Summary





All available functions which can be applied to this `res_list` object:


```r
res_list
```

```
#> A 'ConsensusPartitionList' object with 24 methods.
#>   On a matrix with 18140 rows and 52 columns.
#>   Top rows are extracted by 'SD, CV, MAD, ATC' methods.
#>   Subgroups are detected by 'hclust, kmeans, skmeans, pam, mclust, NMF' method.
#>   Number of partitions are tried for k = 2, 3, 4, 5, 6.
#>   Performed in total 30000 partitions by row resampling.
#> 
#> Following methods can be applied to this 'ConsensusPartitionList' object:
#>  [1] "cola_report"           "collect_classes"       "collect_plots"         "collect_stats"        
#>  [5] "colnames"              "functional_enrichment" "get_anno_col"          "get_anno"             
#>  [9] "get_classes"           "get_matrix"            "get_membership"        "get_stats"            
#> [13] "is_best_k"             "is_stable_k"           "ncol"                  "nrow"                 
#> [17] "rownames"              "show"                  "suggest_best_k"        "test_to_known_factors"
#> [21] "top_rows_heatmap"      "top_rows_overlap"     
#> 
#> You can get result for a single method by, e.g. object["SD", "hclust"] or object["SD:hclust"]
#> or a subset of methods by object[c("SD", "CV")], c("hclust", "kmeans")]
```

The call of `run_all_consensus_partition_methods()` was:


```
#> run_all_consensus_partition_methods(data = mat, mc.cores = 4)
```

Dimension of the input matrix:


```r
mat = get_matrix(res_list)
dim(mat)
```

```
#> [1] 18140    52
```

### Density distribution

The density distribution for each sample is visualized as in one column in the
following heatmap. The clustering is based on the distance which is the
Kolmogorov-Smirnov statistic between two distributions.




```r
library(ComplexHeatmap)
densityHeatmap(mat, ylab = "value", cluster_columns = TRUE, show_column_names = FALSE,
    mc.cores = 4)
```

![plot of chunk density-heatmap](figure_cola/density-heatmap-1.png)





### Suggest the best k



Folowing table shows the best `k` (number of partitions) for each combination
of top-value methods and partition methods. Clicking on the method name in
the table goes to the section for a single combination of methods.

[The cola vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13)
explains the definition of the metrics used for determining the best
number of partitions.


```r
suggest_best_k(res_list)
```


|                            | The best k| 1-PAC| Mean silhouette| Concordance|   |Optional k |
|:---------------------------|----------:|-----:|---------------:|-----------:|:--|:----------|
|[SD:hclust](#SD-hclust)     |          2| 1.000|           1.000|       1.000|** |           |
|[SD:kmeans](#SD-kmeans)     |          2| 1.000|           0.971|       0.973|** |           |
|[SD:mclust](#SD-mclust)     |          2| 1.000|           1.000|       1.000|** |           |
|[CV:hclust](#CV-hclust)     |          2| 1.000|           0.998|       0.999|** |           |
|[CV:kmeans](#CV-kmeans)     |          2| 1.000|           1.000|       1.000|** |           |
|[CV:pam](#CV-pam)           |          2| 1.000|           0.991|       0.996|** |           |
|[MAD:hclust](#MAD-hclust)   |          2| 1.000|           1.000|       1.000|** |           |
|[MAD:mclust](#MAD-mclust)   |          2| 1.000|           0.998|       0.999|** |           |
|[ATC:hclust](#ATC-hclust)   |          2| 1.000|           1.000|       1.000|** |           |
|[ATC:skmeans](#ATC-skmeans) |          2| 1.000|           0.992|       0.996|** |           |
|[CV:mclust](#CV-mclust)     |          2| 0.962|           0.950|       0.980|** |           |
|[ATC:kmeans](#ATC-kmeans)   |          3| 0.962|           0.949|       0.980|** |2          |
|[CV:skmeans](#CV-skmeans)   |          2| 0.960|           0.936|       0.975|** |           |
|[MAD:skmeans](#MAD-skmeans) |          2| 0.959|           0.953|       0.980|** |           |
|[ATC:pam](#ATC-pam)         |          5| 0.918|           0.874|       0.956|*  |2,3,4      |
|[CV:NMF](#CV-NMF)           |          2| 0.910|           0.905|       0.961|*  |           |
|[SD:pam](#SD-pam)           |          4| 0.906|           0.890|       0.954|*  |2          |
|[SD:skmeans](#SD-skmeans)   |          3| 0.889|           0.889|       0.947|   |           |
|[MAD:pam](#MAD-pam)         |          5| 0.808|           0.883|       0.927|   |           |
|[MAD:NMF](#MAD-NMF)         |          2| 0.737|           0.884|       0.951|   |           |
|[SD:NMF](#SD-NMF)           |          2| 0.701|           0.882|       0.946|   |           |
|[ATC:NMF](#ATC-NMF)         |          2| 0.633|           0.810|       0.915|   |           |
|[ATC:mclust](#ATC-mclust)   |          4| 0.570|           0.854|       0.872|   |           |
|[MAD:kmeans](#MAD-kmeans)   |          2| 0.483|           0.817|       0.836|   |           |

\*\*: 1-PAC > 0.95, \*: 1-PAC > 0.9




### CDF of consensus matrices

Cumulative distribution function curves of consensus matrix for all methods.




```r
collect_plots(res_list, fun = plot_ecdf)
```

![plot of chunk collect-plots](figure_cola/collect-plots-1.png)



### Consensus heatmap

Consensus heatmaps for all methods. ([What is a consensus heatmap?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_9))


<style type='text/css'>



.ui-helper-hidden {
	display: none;
}
.ui-helper-hidden-accessible {
	border: 0;
	clip: rect(0 0 0 0);
	height: 1px;
	margin: -1px;
	overflow: hidden;
	padding: 0;
	position: absolute;
	width: 1px;
}
.ui-helper-reset {
	margin: 0;
	padding: 0;
	border: 0;
	outline: 0;
	line-height: 1.3;
	text-decoration: none;
	font-size: 100%;
	list-style: none;
}
.ui-helper-clearfix:before,
.ui-helper-clearfix:after {
	content: "";
	display: table;
	border-collapse: collapse;
}
.ui-helper-clearfix:after {
	clear: both;
}
.ui-helper-zfix {
	width: 100%;
	height: 100%;
	top: 0;
	left: 0;
	position: absolute;
	opacity: 0;
	filter:Alpha(Opacity=0); 
}

.ui-front {
	z-index: 100;
}



.ui-state-disabled {
	cursor: default !important;
	pointer-events: none;
}



.ui-icon {
	display: inline-block;
	vertical-align: middle;
	margin-top: -.25em;
	position: relative;
	text-indent: -99999px;
	overflow: hidden;
	background-repeat: no-repeat;
}

.ui-widget-icon-block {
	left: 50%;
	margin-left: -8px;
	display: block;
}




.ui-widget-overlay {
	position: fixed;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
}
.ui-accordion .ui-accordion-header {
	display: block;
	cursor: pointer;
	position: relative;
	margin: 2px 0 0 0;
	padding: .5em .5em .5em .7em;
	font-size: 100%;
}
.ui-accordion .ui-accordion-content {
	padding: 1em 2.2em;
	border-top: 0;
	overflow: auto;
}
.ui-autocomplete {
	position: absolute;
	top: 0;
	left: 0;
	cursor: default;
}
.ui-menu {
	list-style: none;
	padding: 0;
	margin: 0;
	display: block;
	outline: 0;
}
.ui-menu .ui-menu {
	position: absolute;
}
.ui-menu .ui-menu-item {
	margin: 0;
	cursor: pointer;
	
	list-style-image: url("data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7");
}
.ui-menu .ui-menu-item-wrapper {
	position: relative;
	padding: 3px 1em 3px .4em;
}
.ui-menu .ui-menu-divider {
	margin: 5px 0;
	height: 0;
	font-size: 0;
	line-height: 0;
	border-width: 1px 0 0 0;
}
.ui-menu .ui-state-focus,
.ui-menu .ui-state-active {
	margin: -1px;
}


.ui-menu-icons {
	position: relative;
}
.ui-menu-icons .ui-menu-item-wrapper {
	padding-left: 2em;
}


.ui-menu .ui-icon {
	position: absolute;
	top: 0;
	bottom: 0;
	left: .2em;
	margin: auto 0;
}


.ui-menu .ui-menu-icon {
	left: auto;
	right: 0;
}
.ui-button {
	padding: .4em 1em;
	display: inline-block;
	position: relative;
	line-height: normal;
	margin-right: .1em;
	cursor: pointer;
	vertical-align: middle;
	text-align: center;
	-webkit-user-select: none;
	-moz-user-select: none;
	-ms-user-select: none;
	user-select: none;

	
	overflow: visible;
}

.ui-button,
.ui-button:link,
.ui-button:visited,
.ui-button:hover,
.ui-button:active {
	text-decoration: none;
}


.ui-button-icon-only {
	width: 2em;
	box-sizing: border-box;
	text-indent: -9999px;
	white-space: nowrap;
}


input.ui-button.ui-button-icon-only {
	text-indent: 0;
}


.ui-button-icon-only .ui-icon {
	position: absolute;
	top: 50%;
	left: 50%;
	margin-top: -8px;
	margin-left: -8px;
}

.ui-button.ui-icon-notext .ui-icon {
	padding: 0;
	width: 2.1em;
	height: 2.1em;
	text-indent: -9999px;
	white-space: nowrap;

}

input.ui-button.ui-icon-notext .ui-icon {
	width: auto;
	height: auto;
	text-indent: 0;
	white-space: normal;
	padding: .4em 1em;
}



input.ui-button::-moz-focus-inner,
button.ui-button::-moz-focus-inner {
	border: 0;
	padding: 0;
}
.ui-controlgroup {
	vertical-align: middle;
	display: inline-block;
}
.ui-controlgroup > .ui-controlgroup-item {
	float: left;
	margin-left: 0;
	margin-right: 0;
}
.ui-controlgroup > .ui-controlgroup-item:focus,
.ui-controlgroup > .ui-controlgroup-item.ui-visual-focus {
	z-index: 9999;
}
.ui-controlgroup-vertical > .ui-controlgroup-item {
	display: block;
	float: none;
	width: 100%;
	margin-top: 0;
	margin-bottom: 0;
	text-align: left;
}
.ui-controlgroup-vertical .ui-controlgroup-item {
	box-sizing: border-box;
}
.ui-controlgroup .ui-controlgroup-label {
	padding: .4em 1em;
}
.ui-controlgroup .ui-controlgroup-label span {
	font-size: 80%;
}
.ui-controlgroup-horizontal .ui-controlgroup-label + .ui-controlgroup-item {
	border-left: none;
}
.ui-controlgroup-vertical .ui-controlgroup-label + .ui-controlgroup-item {
	border-top: none;
}
.ui-controlgroup-horizontal .ui-controlgroup-label.ui-widget-content {
	border-right: none;
}
.ui-controlgroup-vertical .ui-controlgroup-label.ui-widget-content {
	border-bottom: none;
}


.ui-controlgroup-vertical .ui-spinner-input {

	
	width: 75%;
	width: calc( 100% - 2.4em );
}
.ui-controlgroup-vertical .ui-spinner .ui-spinner-up {
	border-top-style: solid;
}

.ui-checkboxradio-label .ui-icon-background {
	box-shadow: inset 1px 1px 1px #ccc;
	border-radius: .12em;
	border: none;
}
.ui-checkboxradio-radio-label .ui-icon-background {
	width: 16px;
	height: 16px;
	border-radius: 1em;
	overflow: visible;
	border: none;
}
.ui-checkboxradio-radio-label.ui-checkboxradio-checked .ui-icon,
.ui-checkboxradio-radio-label.ui-checkboxradio-checked:hover .ui-icon {
	background-image: none;
	width: 8px;
	height: 8px;
	border-width: 4px;
	border-style: solid;
}
.ui-checkboxradio-disabled {
	pointer-events: none;
}
.ui-datepicker {
	width: 17em;
	padding: .2em .2em 0;
	display: none;
}
.ui-datepicker .ui-datepicker-header {
	position: relative;
	padding: .2em 0;
}
.ui-datepicker .ui-datepicker-prev,
.ui-datepicker .ui-datepicker-next {
	position: absolute;
	top: 2px;
	width: 1.8em;
	height: 1.8em;
}
.ui-datepicker .ui-datepicker-prev-hover,
.ui-datepicker .ui-datepicker-next-hover {
	top: 1px;
}
.ui-datepicker .ui-datepicker-prev {
	left: 2px;
}
.ui-datepicker .ui-datepicker-next {
	right: 2px;
}
.ui-datepicker .ui-datepicker-prev-hover {
	left: 1px;
}
.ui-datepicker .ui-datepicker-next-hover {
	right: 1px;
}
.ui-datepicker .ui-datepicker-prev span,
.ui-datepicker .ui-datepicker-next span {
	display: block;
	position: absolute;
	left: 50%;
	margin-left: -8px;
	top: 50%;
	margin-top: -8px;
}
.ui-datepicker .ui-datepicker-title {
	margin: 0 2.3em;
	line-height: 1.8em;
	text-align: center;
}
.ui-datepicker .ui-datepicker-title select {
	font-size: 1em;
	margin: 1px 0;
}
.ui-datepicker select.ui-datepicker-month,
.ui-datepicker select.ui-datepicker-year {
	width: 45%;
}
.ui-datepicker table {
	width: 100%;
	font-size: .9em;
	border-collapse: collapse;
	margin: 0 0 .4em;
}
.ui-datepicker th {
	padding: .7em .3em;
	text-align: center;
	font-weight: bold;
	border: 0;
}
.ui-datepicker td {
	border: 0;
	padding: 1px;
}
.ui-datepicker td span,
.ui-datepicker td a {
	display: block;
	padding: .2em;
	text-align: right;
	text-decoration: none;
}
.ui-datepicker .ui-datepicker-buttonpane {
	background-image: none;
	margin: .7em 0 0 0;
	padding: 0 .2em;
	border-left: 0;
	border-right: 0;
	border-bottom: 0;
}
.ui-datepicker .ui-datepicker-buttonpane button {
	float: right;
	margin: .5em .2em .4em;
	cursor: pointer;
	padding: .2em .6em .3em .6em;
	width: auto;
	overflow: visible;
}
.ui-datepicker .ui-datepicker-buttonpane button.ui-datepicker-current {
	float: left;
}


.ui-datepicker.ui-datepicker-multi {
	width: auto;
}
.ui-datepicker-multi .ui-datepicker-group {
	float: left;
}
.ui-datepicker-multi .ui-datepicker-group table {
	width: 95%;
	margin: 0 auto .4em;
}
.ui-datepicker-multi-2 .ui-datepicker-group {
	width: 50%;
}
.ui-datepicker-multi-3 .ui-datepicker-group {
	width: 33.3%;
}
.ui-datepicker-multi-4 .ui-datepicker-group {
	width: 25%;
}
.ui-datepicker-multi .ui-datepicker-group-last .ui-datepicker-header,
.ui-datepicker-multi .ui-datepicker-group-middle .ui-datepicker-header {
	border-left-width: 0;
}
.ui-datepicker-multi .ui-datepicker-buttonpane {
	clear: left;
}
.ui-datepicker-row-break {
	clear: both;
	width: 100%;
	font-size: 0;
}


.ui-datepicker-rtl {
	direction: rtl;
}
.ui-datepicker-rtl .ui-datepicker-prev {
	right: 2px;
	left: auto;
}
.ui-datepicker-rtl .ui-datepicker-next {
	left: 2px;
	right: auto;
}
.ui-datepicker-rtl .ui-datepicker-prev:hover {
	right: 1px;
	left: auto;
}
.ui-datepicker-rtl .ui-datepicker-next:hover {
	left: 1px;
	right: auto;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane {
	clear: right;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane button {
	float: left;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane button.ui-datepicker-current,
.ui-datepicker-rtl .ui-datepicker-group {
	float: right;
}
.ui-datepicker-rtl .ui-datepicker-group-last .ui-datepicker-header,
.ui-datepicker-rtl .ui-datepicker-group-middle .ui-datepicker-header {
	border-right-width: 0;
	border-left-width: 1px;
}


.ui-datepicker .ui-icon {
	display: block;
	text-indent: -99999px;
	overflow: hidden;
	background-repeat: no-repeat;
	left: .5em;
	top: .3em;
}
.ui-dialog {
	position: absolute;
	top: 0;
	left: 0;
	padding: .2em;
	outline: 0;
}
.ui-dialog .ui-dialog-titlebar {
	padding: .4em 1em;
	position: relative;
}
.ui-dialog .ui-dialog-title {
	float: left;
	margin: .1em 0;
	white-space: nowrap;
	width: 90%;
	overflow: hidden;
	text-overflow: ellipsis;
}
.ui-dialog .ui-dialog-titlebar-close {
	position: absolute;
	right: .3em;
	top: 50%;
	width: 20px;
	margin: -10px 0 0 0;
	padding: 1px;
	height: 20px;
}
.ui-dialog .ui-dialog-content {
	position: relative;
	border: 0;
	padding: .5em 1em;
	background: none;
	overflow: auto;
}
.ui-dialog .ui-dialog-buttonpane {
	text-align: left;
	border-width: 1px 0 0 0;
	background-image: none;
	margin-top: .5em;
	padding: .3em 1em .5em .4em;
}
.ui-dialog .ui-dialog-buttonpane .ui-dialog-buttonset {
	float: right;
}
.ui-dialog .ui-dialog-buttonpane button {
	margin: .5em .4em .5em 0;
	cursor: pointer;
}
.ui-dialog .ui-resizable-n {
	height: 2px;
	top: 0;
}
.ui-dialog .ui-resizable-e {
	width: 2px;
	right: 0;
}
.ui-dialog .ui-resizable-s {
	height: 2px;
	bottom: 0;
}
.ui-dialog .ui-resizable-w {
	width: 2px;
	left: 0;
}
.ui-dialog .ui-resizable-se,
.ui-dialog .ui-resizable-sw,
.ui-dialog .ui-resizable-ne,
.ui-dialog .ui-resizable-nw {
	width: 7px;
	height: 7px;
}
.ui-dialog .ui-resizable-se {
	right: 0;
	bottom: 0;
}
.ui-dialog .ui-resizable-sw {
	left: 0;
	bottom: 0;
}
.ui-dialog .ui-resizable-ne {
	right: 0;
	top: 0;
}
.ui-dialog .ui-resizable-nw {
	left: 0;
	top: 0;
}
.ui-draggable .ui-dialog-titlebar {
	cursor: move;
}
.ui-draggable-handle {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-resizable {
	position: relative;
}
.ui-resizable-handle {
	position: absolute;
	font-size: 0.1px;
	display: block;
	-ms-touch-action: none;
	touch-action: none;
}
.ui-resizable-disabled .ui-resizable-handle,
.ui-resizable-autohide .ui-resizable-handle {
	display: none;
}
.ui-resizable-n {
	cursor: n-resize;
	height: 7px;
	width: 100%;
	top: -5px;
	left: 0;
}
.ui-resizable-s {
	cursor: s-resize;
	height: 7px;
	width: 100%;
	bottom: -5px;
	left: 0;
}
.ui-resizable-e {
	cursor: e-resize;
	width: 7px;
	right: -5px;
	top: 0;
	height: 100%;
}
.ui-resizable-w {
	cursor: w-resize;
	width: 7px;
	left: -5px;
	top: 0;
	height: 100%;
}
.ui-resizable-se {
	cursor: se-resize;
	width: 12px;
	height: 12px;
	right: 1px;
	bottom: 1px;
}
.ui-resizable-sw {
	cursor: sw-resize;
	width: 9px;
	height: 9px;
	left: -5px;
	bottom: -5px;
}
.ui-resizable-nw {
	cursor: nw-resize;
	width: 9px;
	height: 9px;
	left: -5px;
	top: -5px;
}
.ui-resizable-ne {
	cursor: ne-resize;
	width: 9px;
	height: 9px;
	right: -5px;
	top: -5px;
}
.ui-progressbar {
	height: 2em;
	text-align: left;
	overflow: hidden;
}
.ui-progressbar .ui-progressbar-value {
	margin: -1px;
	height: 100%;
}
.ui-progressbar .ui-progressbar-overlay {
	background: url("data:image/gif;base64,R0lGODlhKAAoAIABAAAAAP///yH/C05FVFNDQVBFMi4wAwEAAAAh+QQJAQABACwAAAAAKAAoAAACkYwNqXrdC52DS06a7MFZI+4FHBCKoDeWKXqymPqGqxvJrXZbMx7Ttc+w9XgU2FB3lOyQRWET2IFGiU9m1frDVpxZZc6bfHwv4c1YXP6k1Vdy292Fb6UkuvFtXpvWSzA+HycXJHUXiGYIiMg2R6W459gnWGfHNdjIqDWVqemH2ekpObkpOlppWUqZiqr6edqqWQAAIfkECQEAAQAsAAAAACgAKAAAApSMgZnGfaqcg1E2uuzDmmHUBR8Qil95hiPKqWn3aqtLsS18y7G1SzNeowWBENtQd+T1JktP05nzPTdJZlR6vUxNWWjV+vUWhWNkWFwxl9VpZRedYcflIOLafaa28XdsH/ynlcc1uPVDZxQIR0K25+cICCmoqCe5mGhZOfeYSUh5yJcJyrkZWWpaR8doJ2o4NYq62lAAACH5BAkBAAEALAAAAAAoACgAAAKVDI4Yy22ZnINRNqosw0Bv7i1gyHUkFj7oSaWlu3ovC8GxNso5fluz3qLVhBVeT/Lz7ZTHyxL5dDalQWPVOsQWtRnuwXaFTj9jVVh8pma9JjZ4zYSj5ZOyma7uuolffh+IR5aW97cHuBUXKGKXlKjn+DiHWMcYJah4N0lYCMlJOXipGRr5qdgoSTrqWSq6WFl2ypoaUAAAIfkECQEAAQAsAAAAACgAKAAAApaEb6HLgd/iO7FNWtcFWe+ufODGjRfoiJ2akShbueb0wtI50zm02pbvwfWEMWBQ1zKGlLIhskiEPm9R6vRXxV4ZzWT2yHOGpWMyorblKlNp8HmHEb/lCXjcW7bmtXP8Xt229OVWR1fod2eWqNfHuMjXCPkIGNileOiImVmCOEmoSfn3yXlJWmoHGhqp6ilYuWYpmTqKUgAAIfkECQEAAQAsAAAAACgAKAAAApiEH6kb58biQ3FNWtMFWW3eNVcojuFGfqnZqSebuS06w5V80/X02pKe8zFwP6EFWOT1lDFk8rGERh1TTNOocQ61Hm4Xm2VexUHpzjymViHrFbiELsefVrn6XKfnt2Q9G/+Xdie499XHd2g4h7ioOGhXGJboGAnXSBnoBwKYyfioubZJ2Hn0RuRZaflZOil56Zp6iioKSXpUAAAh+QQJAQABACwAAAAAKAAoAAACkoQRqRvnxuI7kU1a1UU5bd5tnSeOZXhmn5lWK3qNTWvRdQxP8qvaC+/yaYQzXO7BMvaUEmJRd3TsiMAgswmNYrSgZdYrTX6tSHGZO73ezuAw2uxuQ+BbeZfMxsexY35+/Qe4J1inV0g4x3WHuMhIl2jXOKT2Q+VU5fgoSUI52VfZyfkJGkha6jmY+aaYdirq+lQAACH5BAkBAAEALAAAAAAoACgAAAKWBIKpYe0L3YNKToqswUlvznigd4wiR4KhZrKt9Upqip61i9E3vMvxRdHlbEFiEXfk9YARYxOZZD6VQ2pUunBmtRXo1Lf8hMVVcNl8JafV38aM2/Fu5V16Bn63r6xt97j09+MXSFi4BniGFae3hzbH9+hYBzkpuUh5aZmHuanZOZgIuvbGiNeomCnaxxap2upaCZsq+1kAACH5BAkBAAEALAAAAAAoACgAAAKXjI8By5zf4kOxTVrXNVlv1X0d8IGZGKLnNpYtm8Lr9cqVeuOSvfOW79D9aDHizNhDJidFZhNydEahOaDH6nomtJjp1tutKoNWkvA6JqfRVLHU/QUfau9l2x7G54d1fl995xcIGAdXqMfBNadoYrhH+Mg2KBlpVpbluCiXmMnZ2Sh4GBqJ+ckIOqqJ6LmKSllZmsoq6wpQAAAh+QQJAQABACwAAAAAKAAoAAAClYx/oLvoxuJDkU1a1YUZbJ59nSd2ZXhWqbRa2/gF8Gu2DY3iqs7yrq+xBYEkYvFSM8aSSObE+ZgRl1BHFZNr7pRCavZ5BW2142hY3AN/zWtsmf12p9XxxFl2lpLn1rseztfXZjdIWIf2s5dItwjYKBgo9yg5pHgzJXTEeGlZuenpyPmpGQoKOWkYmSpaSnqKileI2FAAACH5BAkBAAEALAAAAAAoACgAAAKVjB+gu+jG4kORTVrVhRlsnn2dJ3ZleFaptFrb+CXmO9OozeL5VfP99HvAWhpiUdcwkpBH3825AwYdU8xTqlLGhtCosArKMpvfa1mMRae9VvWZfeB2XfPkeLmm18lUcBj+p5dnN8jXZ3YIGEhYuOUn45aoCDkp16hl5IjYJvjWKcnoGQpqyPlpOhr3aElaqrq56Bq7VAAAOw==");
	height: 100%;
	filter: alpha(opacity=25); 
	opacity: 0.25;
}
.ui-progressbar-indeterminate .ui-progressbar-value {
	background-image: none;
}
.ui-selectable {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-selectable-helper {
	position: absolute;
	z-index: 100;
	border: 1px dotted black;
}
.ui-selectmenu-menu {
	padding: 0;
	margin: 0;
	position: absolute;
	top: 0;
	left: 0;
	display: none;
}
.ui-selectmenu-menu .ui-menu {
	overflow: auto;
	overflow-x: hidden;
	padding-bottom: 1px;
}
.ui-selectmenu-menu .ui-menu .ui-selectmenu-optgroup {
	font-size: 1em;
	font-weight: bold;
	line-height: 1.5;
	padding: 2px 0.4em;
	margin: 0.5em 0 0 0;
	height: auto;
	border: 0;
}
.ui-selectmenu-open {
	display: block;
}
.ui-selectmenu-text {
	display: block;
	margin-right: 20px;
	overflow: hidden;
	text-overflow: ellipsis;
}
.ui-selectmenu-button.ui-button {
	text-align: left;
	white-space: nowrap;
	width: 14em;
}
.ui-selectmenu-icon.ui-icon {
	float: right;
	margin-top: 0;
}
.ui-slider {
	position: relative;
	text-align: left;
}
.ui-slider .ui-slider-handle {
	position: absolute;
	z-index: 2;
	width: 1.2em;
	height: 1.2em;
	cursor: default;
	-ms-touch-action: none;
	touch-action: none;
}
.ui-slider .ui-slider-range {
	position: absolute;
	z-index: 1;
	font-size: .7em;
	display: block;
	border: 0;
	background-position: 0 0;
}


.ui-slider.ui-state-disabled .ui-slider-handle,
.ui-slider.ui-state-disabled .ui-slider-range {
	filter: inherit;
}

.ui-slider-horizontal {
	height: .8em;
}
.ui-slider-horizontal .ui-slider-handle {
	top: -.3em;
	margin-left: -.6em;
}
.ui-slider-horizontal .ui-slider-range {
	top: 0;
	height: 100%;
}
.ui-slider-horizontal .ui-slider-range-min {
	left: 0;
}
.ui-slider-horizontal .ui-slider-range-max {
	right: 0;
}

.ui-slider-vertical {
	width: .8em;
	height: 100px;
}
.ui-slider-vertical .ui-slider-handle {
	left: -.3em;
	margin-left: 0;
	margin-bottom: -.6em;
}
.ui-slider-vertical .ui-slider-range {
	left: 0;
	width: 100%;
}
.ui-slider-vertical .ui-slider-range-min {
	bottom: 0;
}
.ui-slider-vertical .ui-slider-range-max {
	top: 0;
}
.ui-sortable-handle {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-spinner {
	position: relative;
	display: inline-block;
	overflow: hidden;
	padding: 0;
	vertical-align: middle;
}
.ui-spinner-input {
	border: none;
	background: none;
	color: inherit;
	padding: .222em 0;
	margin: .2em 0;
	vertical-align: middle;
	margin-left: .4em;
	margin-right: 2em;
}
.ui-spinner-button {
	width: 1.6em;
	height: 50%;
	font-size: .5em;
	padding: 0;
	margin: 0;
	text-align: center;
	position: absolute;
	cursor: default;
	display: block;
	overflow: hidden;
	right: 0;
}

.ui-spinner a.ui-spinner-button {
	border-top-style: none;
	border-bottom-style: none;
	border-right-style: none;
}
.ui-spinner-up {
	top: 0;
}
.ui-spinner-down {
	bottom: 0;
}
.ui-tabs {
	position: relative;
	padding: .2em;
}
.ui-tabs .ui-tabs-nav {
	margin: 0;
	padding: .2em .2em 0;
}
.ui-tabs .ui-tabs-nav li {
	list-style: none;
	float: left;
	position: relative;
	top: 0;
	margin: 1px .2em 0 0;
	border-bottom-width: 0;
	padding: 0;
	white-space: nowrap;
}
.ui-tabs .ui-tabs-nav .ui-tabs-anchor {
	float: left;
	padding: .5em 1em;
	text-decoration: none;
}
.ui-tabs .ui-tabs-nav li.ui-tabs-active {
	margin-bottom: -1px;
	padding-bottom: 1px;
}
.ui-tabs .ui-tabs-nav li.ui-tabs-active .ui-tabs-anchor,
.ui-tabs .ui-tabs-nav li.ui-state-disabled .ui-tabs-anchor,
.ui-tabs .ui-tabs-nav li.ui-tabs-loading .ui-tabs-anchor {
	cursor: text;
}
.ui-tabs-collapsible .ui-tabs-nav li.ui-tabs-active .ui-tabs-anchor {
	cursor: pointer;
}
.ui-tabs .ui-tabs-panel {
	display: block;
	border-width: 0;
	padding: 1em 1.4em;
	background: none;
}
.ui-tooltip {
	padding: 8px;
	position: absolute;
	z-index: 9999;
	max-width: 300px;
}
body .ui-tooltip {
	border-width: 2px;
}

.ui-widget {
	font-family: Arial,Helvetica,sans-serif;
	font-size: 1em;
}
.ui-widget .ui-widget {
	font-size: 1em;
}
.ui-widget input,
.ui-widget select,
.ui-widget textarea,
.ui-widget button {
	font-family: Arial,Helvetica,sans-serif;
	font-size: 1em;
}
.ui-widget.ui-widget-content {
	border: 1px solid #c5c5c5;
}
.ui-widget-content {
	border: 1px solid #dddddd;
	background: #ffffff;
	color: #333333;
}
.ui-widget-content a {
	color: #333333;
}
.ui-widget-header {
	border: 1px solid #dddddd;
	background: #e9e9e9;
	color: #333333;
	font-weight: bold;
}
.ui-widget-header a {
	color: #333333;
}


.ui-state-default,
.ui-widget-content .ui-state-default,
.ui-widget-header .ui-state-default,
.ui-button,


html .ui-button.ui-state-disabled:hover,
html .ui-button.ui-state-disabled:active {
	border: 1px solid #c5c5c5;
	background: #f6f6f6;
	font-weight: normal;
	color: #454545;
}
.ui-state-default a,
.ui-state-default a:link,
.ui-state-default a:visited,
a.ui-button,
a:link.ui-button,
a:visited.ui-button,
.ui-button {
	color: #454545;
	text-decoration: none;
}
.ui-state-hover,
.ui-widget-content .ui-state-hover,
.ui-widget-header .ui-state-hover,
.ui-state-focus,
.ui-widget-content .ui-state-focus,
.ui-widget-header .ui-state-focus,
.ui-button:hover,
.ui-button:focus {
	border: 1px solid #cccccc;
	background: #ededed;
	font-weight: normal;
	color: #2b2b2b;
}
.ui-state-hover a,
.ui-state-hover a:hover,
.ui-state-hover a:link,
.ui-state-hover a:visited,
.ui-state-focus a,
.ui-state-focus a:hover,
.ui-state-focus a:link,
.ui-state-focus a:visited,
a.ui-button:hover,
a.ui-button:focus {
	color: #2b2b2b;
	text-decoration: none;
}

.ui-visual-focus {
	box-shadow: 0 0 3px 1px rgb(94, 158, 214);
}
.ui-state-active,
.ui-widget-content .ui-state-active,
.ui-widget-header .ui-state-active,
a.ui-button:active,
.ui-button:active,
.ui-button.ui-state-active:hover {
	border: 1px solid #003eff;
	background: #007fff;
	font-weight: normal;
	color: #ffffff;
}
.ui-icon-background,
.ui-state-active .ui-icon-background {
	border: #003eff;
	background-color: #ffffff;
}
.ui-state-active a,
.ui-state-active a:link,
.ui-state-active a:visited {
	color: #ffffff;
	text-decoration: none;
}


.ui-state-highlight,
.ui-widget-content .ui-state-highlight,
.ui-widget-header .ui-state-highlight {
	border: 1px solid #dad55e;
	background: #fffa90;
	color: #777620;
}
.ui-state-checked {
	border: 1px solid #dad55e;
	background: #fffa90;
}
.ui-state-highlight a,
.ui-widget-content .ui-state-highlight a,
.ui-widget-header .ui-state-highlight a {
	color: #777620;
}
.ui-state-error,
.ui-widget-content .ui-state-error,
.ui-widget-header .ui-state-error {
	border: 1px solid #f1a899;
	background: #fddfdf;
	color: #5f3f3f;
}
.ui-state-error a,
.ui-widget-content .ui-state-error a,
.ui-widget-header .ui-state-error a {
	color: #5f3f3f;
}
.ui-state-error-text,
.ui-widget-content .ui-state-error-text,
.ui-widget-header .ui-state-error-text {
	color: #5f3f3f;
}
.ui-priority-primary,
.ui-widget-content .ui-priority-primary,
.ui-widget-header .ui-priority-primary {
	font-weight: bold;
}
.ui-priority-secondary,
.ui-widget-content .ui-priority-secondary,
.ui-widget-header .ui-priority-secondary {
	opacity: .7;
	filter:Alpha(Opacity=70); 
	font-weight: normal;
}
.ui-state-disabled,
.ui-widget-content .ui-state-disabled,
.ui-widget-header .ui-state-disabled {
	opacity: .35;
	filter:Alpha(Opacity=35); 
	background-image: none;
}
.ui-state-disabled .ui-icon {
	filter:Alpha(Opacity=35); 
}




.ui-icon {
	width: 16px;
	height: 16px;
}
.ui-icon,
.ui-widget-content .ui-icon {
	background-image: url("images/ui-icons_444444_256x240.png");
}
.ui-widget-header .ui-icon {
	background-image: url("images/ui-icons_444444_256x240.png");
}
.ui-state-hover .ui-icon,
.ui-state-focus .ui-icon,
.ui-button:hover .ui-icon,
.ui-button:focus .ui-icon {
	background-image: url("images/ui-icons_555555_256x240.png");
}
.ui-state-active .ui-icon,
.ui-button:active .ui-icon {
	background-image: url("images/ui-icons_ffffff_256x240.png");
}
.ui-state-highlight .ui-icon,
.ui-button .ui-state-highlight.ui-icon {
	background-image: url("images/ui-icons_777620_256x240.png");
}
.ui-state-error .ui-icon,
.ui-state-error-text .ui-icon {
	background-image: url("images/ui-icons_cc0000_256x240.png");
}
.ui-button .ui-icon {
	background-image: url("images/ui-icons_777777_256x240.png");
}


.ui-icon-blank { background-position: 16px 16px; }
.ui-icon-caret-1-n { background-position: 0 0; }
.ui-icon-caret-1-ne { background-position: -16px 0; }
.ui-icon-caret-1-e { background-position: -32px 0; }
.ui-icon-caret-1-se { background-position: -48px 0; }
.ui-icon-caret-1-s { background-position: -65px 0; }
.ui-icon-caret-1-sw { background-position: -80px 0; }
.ui-icon-caret-1-w { background-position: -96px 0; }
.ui-icon-caret-1-nw { background-position: -112px 0; }
.ui-icon-caret-2-n-s { background-position: -128px 0; }
.ui-icon-caret-2-e-w { background-position: -144px 0; }
.ui-icon-triangle-1-n { background-position: 0 -16px; }
.ui-icon-triangle-1-ne { background-position: -16px -16px; }
.ui-icon-triangle-1-e { background-position: -32px -16px; }
.ui-icon-triangle-1-se { background-position: -48px -16px; }
.ui-icon-triangle-1-s { background-position: -65px -16px; }
.ui-icon-triangle-1-sw { background-position: -80px -16px; }
.ui-icon-triangle-1-w { background-position: -96px -16px; }
.ui-icon-triangle-1-nw { background-position: -112px -16px; }
.ui-icon-triangle-2-n-s { background-position: -128px -16px; }
.ui-icon-triangle-2-e-w { background-position: -144px -16px; }
.ui-icon-arrow-1-n { background-position: 0 -32px; }
.ui-icon-arrow-1-ne { background-position: -16px -32px; }
.ui-icon-arrow-1-e { background-position: -32px -32px; }
.ui-icon-arrow-1-se { background-position: -48px -32px; }
.ui-icon-arrow-1-s { background-position: -65px -32px; }
.ui-icon-arrow-1-sw { background-position: -80px -32px; }
.ui-icon-arrow-1-w { background-position: -96px -32px; }
.ui-icon-arrow-1-nw { background-position: -112px -32px; }
.ui-icon-arrow-2-n-s { background-position: -128px -32px; }
.ui-icon-arrow-2-ne-sw { background-position: -144px -32px; }
.ui-icon-arrow-2-e-w { background-position: -160px -32px; }
.ui-icon-arrow-2-se-nw { background-position: -176px -32px; }
.ui-icon-arrowstop-1-n { background-position: -192px -32px; }
.ui-icon-arrowstop-1-e { background-position: -208px -32px; }
.ui-icon-arrowstop-1-s { background-position: -224px -32px; }
.ui-icon-arrowstop-1-w { background-position: -240px -32px; }
.ui-icon-arrowthick-1-n { background-position: 1px -48px; }
.ui-icon-arrowthick-1-ne { background-position: -16px -48px; }
.ui-icon-arrowthick-1-e { background-position: -32px -48px; }
.ui-icon-arrowthick-1-se { background-position: -48px -48px; }
.ui-icon-arrowthick-1-s { background-position: -64px -48px; }
.ui-icon-arrowthick-1-sw { background-position: -80px -48px; }
.ui-icon-arrowthick-1-w { background-position: -96px -48px; }
.ui-icon-arrowthick-1-nw { background-position: -112px -48px; }
.ui-icon-arrowthick-2-n-s { background-position: -128px -48px; }
.ui-icon-arrowthick-2-ne-sw { background-position: -144px -48px; }
.ui-icon-arrowthick-2-e-w { background-position: -160px -48px; }
.ui-icon-arrowthick-2-se-nw { background-position: -176px -48px; }
.ui-icon-arrowthickstop-1-n { background-position: -192px -48px; }
.ui-icon-arrowthickstop-1-e { background-position: -208px -48px; }
.ui-icon-arrowthickstop-1-s { background-position: -224px -48px; }
.ui-icon-arrowthickstop-1-w { background-position: -240px -48px; }
.ui-icon-arrowreturnthick-1-w { background-position: 0 -64px; }
.ui-icon-arrowreturnthick-1-n { background-position: -16px -64px; }
.ui-icon-arrowreturnthick-1-e { background-position: -32px -64px; }
.ui-icon-arrowreturnthick-1-s { background-position: -48px -64px; }
.ui-icon-arrowreturn-1-w { background-position: -64px -64px; }
.ui-icon-arrowreturn-1-n { background-position: -80px -64px; }
.ui-icon-arrowreturn-1-e { background-position: -96px -64px; }
.ui-icon-arrowreturn-1-s { background-position: -112px -64px; }
.ui-icon-arrowrefresh-1-w { background-position: -128px -64px; }
.ui-icon-arrowrefresh-1-n { background-position: -144px -64px; }
.ui-icon-arrowrefresh-1-e { background-position: -160px -64px; }
.ui-icon-arrowrefresh-1-s { background-position: -176px -64px; }
.ui-icon-arrow-4 { background-position: 0 -80px; }
.ui-icon-arrow-4-diag { background-position: -16px -80px; }
.ui-icon-extlink { background-position: -32px -80px; }
.ui-icon-newwin { background-position: -48px -80px; }
.ui-icon-refresh { background-position: -64px -80px; }
.ui-icon-shuffle { background-position: -80px -80px; }
.ui-icon-transfer-e-w { background-position: -96px -80px; }
.ui-icon-transferthick-e-w { background-position: -112px -80px; }
.ui-icon-folder-collapsed { background-position: 0 -96px; }
.ui-icon-folder-open { background-position: -16px -96px; }
.ui-icon-document { background-position: -32px -96px; }
.ui-icon-document-b { background-position: -48px -96px; }
.ui-icon-note { background-position: -64px -96px; }
.ui-icon-mail-closed { background-position: -80px -96px; }
.ui-icon-mail-open { background-position: -96px -96px; }
.ui-icon-suitcase { background-position: -112px -96px; }
.ui-icon-comment { background-position: -128px -96px; }
.ui-icon-person { background-position: -144px -96px; }
.ui-icon-print { background-position: -160px -96px; }
.ui-icon-trash { background-position: -176px -96px; }
.ui-icon-locked { background-position: -192px -96px; }
.ui-icon-unlocked { background-position: -208px -96px; }
.ui-icon-bookmark { background-position: -224px -96px; }
.ui-icon-tag { background-position: -240px -96px; }
.ui-icon-home { background-position: 0 -112px; }
.ui-icon-flag { background-position: -16px -112px; }
.ui-icon-calendar { background-position: -32px -112px; }
.ui-icon-cart { background-position: -48px -112px; }
.ui-icon-pencil { background-position: -64px -112px; }
.ui-icon-clock { background-position: -80px -112px; }
.ui-icon-disk { background-position: -96px -112px; }
.ui-icon-calculator { background-position: -112px -112px; }
.ui-icon-zoomin { background-position: -128px -112px; }
.ui-icon-zoomout { background-position: -144px -112px; }
.ui-icon-search { background-position: -160px -112px; }
.ui-icon-wrench { background-position: -176px -112px; }
.ui-icon-gear { background-position: -192px -112px; }
.ui-icon-heart { background-position: -208px -112px; }
.ui-icon-star { background-position: -224px -112px; }
.ui-icon-link { background-position: -240px -112px; }
.ui-icon-cancel { background-position: 0 -128px; }
.ui-icon-plus { background-position: -16px -128px; }
.ui-icon-plusthick { background-position: -32px -128px; }
.ui-icon-minus { background-position: -48px -128px; }
.ui-icon-minusthick { background-position: -64px -128px; }
.ui-icon-close { background-position: -80px -128px; }
.ui-icon-closethick { background-position: -96px -128px; }
.ui-icon-key { background-position: -112px -128px; }
.ui-icon-lightbulb { background-position: -128px -128px; }
.ui-icon-scissors { background-position: -144px -128px; }
.ui-icon-clipboard { background-position: -160px -128px; }
.ui-icon-copy { background-position: -176px -128px; }
.ui-icon-contact { background-position: -192px -128px; }
.ui-icon-image { background-position: -208px -128px; }
.ui-icon-video { background-position: -224px -128px; }
.ui-icon-script { background-position: -240px -128px; }
.ui-icon-alert { background-position: 0 -144px; }
.ui-icon-info { background-position: -16px -144px; }
.ui-icon-notice { background-position: -32px -144px; }
.ui-icon-help { background-position: -48px -144px; }
.ui-icon-check { background-position: -64px -144px; }
.ui-icon-bullet { background-position: -80px -144px; }
.ui-icon-radio-on { background-position: -96px -144px; }
.ui-icon-radio-off { background-position: -112px -144px; }
.ui-icon-pin-w { background-position: -128px -144px; }
.ui-icon-pin-s { background-position: -144px -144px; }
.ui-icon-play { background-position: 0 -160px; }
.ui-icon-pause { background-position: -16px -160px; }
.ui-icon-seek-next { background-position: -32px -160px; }
.ui-icon-seek-prev { background-position: -48px -160px; }
.ui-icon-seek-end { background-position: -64px -160px; }
.ui-icon-seek-start { background-position: -80px -160px; }

.ui-icon-seek-first { background-position: -80px -160px; }
.ui-icon-stop { background-position: -96px -160px; }
.ui-icon-eject { background-position: -112px -160px; }
.ui-icon-volume-off { background-position: -128px -160px; }
.ui-icon-volume-on { background-position: -144px -160px; }
.ui-icon-power { background-position: 0 -176px; }
.ui-icon-signal-diag { background-position: -16px -176px; }
.ui-icon-signal { background-position: -32px -176px; }
.ui-icon-battery-0 { background-position: -48px -176px; }
.ui-icon-battery-1 { background-position: -64px -176px; }
.ui-icon-battery-2 { background-position: -80px -176px; }
.ui-icon-battery-3 { background-position: -96px -176px; }
.ui-icon-circle-plus { background-position: 0 -192px; }
.ui-icon-circle-minus { background-position: -16px -192px; }
.ui-icon-circle-close { background-position: -32px -192px; }
.ui-icon-circle-triangle-e { background-position: -48px -192px; }
.ui-icon-circle-triangle-s { background-position: -64px -192px; }
.ui-icon-circle-triangle-w { background-position: -80px -192px; }
.ui-icon-circle-triangle-n { background-position: -96px -192px; }
.ui-icon-circle-arrow-e { background-position: -112px -192px; }
.ui-icon-circle-arrow-s { background-position: -128px -192px; }
.ui-icon-circle-arrow-w { background-position: -144px -192px; }
.ui-icon-circle-arrow-n { background-position: -160px -192px; }
.ui-icon-circle-zoomin { background-position: -176px -192px; }
.ui-icon-circle-zoomout { background-position: -192px -192px; }
.ui-icon-circle-check { background-position: -208px -192px; }
.ui-icon-circlesmall-plus { background-position: 0 -208px; }
.ui-icon-circlesmall-minus { background-position: -16px -208px; }
.ui-icon-circlesmall-close { background-position: -32px -208px; }
.ui-icon-squaresmall-plus { background-position: -48px -208px; }
.ui-icon-squaresmall-minus { background-position: -64px -208px; }
.ui-icon-squaresmall-close { background-position: -80px -208px; }
.ui-icon-grip-dotted-vertical { background-position: 0 -224px; }
.ui-icon-grip-dotted-horizontal { background-position: -16px -224px; }
.ui-icon-grip-solid-vertical { background-position: -32px -224px; }
.ui-icon-grip-solid-horizontal { background-position: -48px -224px; }
.ui-icon-gripsmall-diagonal-se { background-position: -64px -224px; }
.ui-icon-grip-diagonal-se { background-position: -80px -224px; }





.ui-corner-all,
.ui-corner-top,
.ui-corner-left,
.ui-corner-tl {
	border-top-left-radius: 3px;
}
.ui-corner-all,
.ui-corner-top,
.ui-corner-right,
.ui-corner-tr {
	border-top-right-radius: 3px;
}
.ui-corner-all,
.ui-corner-bottom,
.ui-corner-left,
.ui-corner-bl {
	border-bottom-left-radius: 3px;
}
.ui-corner-all,
.ui-corner-bottom,
.ui-corner-right,
.ui-corner-br {
	border-bottom-right-radius: 3px;
}


.ui-widget-overlay {
	background: #aaaaaa;
	opacity: .3;
	filter: Alpha(Opacity=30); 
}
.ui-widget-shadow {
	-webkit-box-shadow: 0px 0px 5px #666666;
	box-shadow: 0px 0px 5px #666666;
} 
</style>
<script src='js/jquery-1.12.4.js'></script>
<script src='js/jquery-ui.js'></script>

<script>
$( function() {
	$( '#tabs-collect-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-collect-consensus-heatmap'>
<ul>
<li><a href='#tab-collect-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-collect-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-collect-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-collect-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-collect-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-collect-consensus-heatmap-1'>
<pre><code class="r">collect_plots(res_list, k = 2, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-1-1.png" alt="plot of chunk tab-collect-consensus-heatmap-1"/></p>

</div>
<div id='tab-collect-consensus-heatmap-2'>
<pre><code class="r">collect_plots(res_list, k = 3, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-2-1.png" alt="plot of chunk tab-collect-consensus-heatmap-2"/></p>

</div>
<div id='tab-collect-consensus-heatmap-3'>
<pre><code class="r">collect_plots(res_list, k = 4, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-3-1.png" alt="plot of chunk tab-collect-consensus-heatmap-3"/></p>

</div>
<div id='tab-collect-consensus-heatmap-4'>
<pre><code class="r">collect_plots(res_list, k = 5, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-4-1.png" alt="plot of chunk tab-collect-consensus-heatmap-4"/></p>

</div>
<div id='tab-collect-consensus-heatmap-5'>
<pre><code class="r">collect_plots(res_list, k = 6, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-5-1.png" alt="plot of chunk tab-collect-consensus-heatmap-5"/></p>

</div>
</div>



### Membership heatmap

Membership heatmaps for all methods. ([What is a membership heatmap?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_12))


<script>
$( function() {
	$( '#tabs-collect-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-collect-membership-heatmap'>
<ul>
<li><a href='#tab-collect-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-collect-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-collect-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-collect-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-collect-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-collect-membership-heatmap-1'>
<pre><code class="r">collect_plots(res_list, k = 2, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-1-1.png" alt="plot of chunk tab-collect-membership-heatmap-1"/></p>

</div>
<div id='tab-collect-membership-heatmap-2'>
<pre><code class="r">collect_plots(res_list, k = 3, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-2-1.png" alt="plot of chunk tab-collect-membership-heatmap-2"/></p>

</div>
<div id='tab-collect-membership-heatmap-3'>
<pre><code class="r">collect_plots(res_list, k = 4, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-3-1.png" alt="plot of chunk tab-collect-membership-heatmap-3"/></p>

</div>
<div id='tab-collect-membership-heatmap-4'>
<pre><code class="r">collect_plots(res_list, k = 5, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-4-1.png" alt="plot of chunk tab-collect-membership-heatmap-4"/></p>

</div>
<div id='tab-collect-membership-heatmap-5'>
<pre><code class="r">collect_plots(res_list, k = 6, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-5-1.png" alt="plot of chunk tab-collect-membership-heatmap-5"/></p>

</div>
</div>



### Signature heatmap

Signature heatmaps for all methods. ([What is a signature heatmap?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_22))


Note in following heatmaps, rows are scaled.



<script>
$( function() {
	$( '#tabs-collect-get-signatures' ).tabs();
} );
</script>
<div id='tabs-collect-get-signatures'>
<ul>
<li><a href='#tab-collect-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-collect-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-collect-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-collect-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-collect-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-collect-get-signatures-1'>
<pre><code class="r">collect_plots(res_list, k = 2, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-1-1.png" alt="plot of chunk tab-collect-get-signatures-1"/></p>

</div>
<div id='tab-collect-get-signatures-2'>
<pre><code class="r">collect_plots(res_list, k = 3, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-2-1.png" alt="plot of chunk tab-collect-get-signatures-2"/></p>

</div>
<div id='tab-collect-get-signatures-3'>
<pre><code class="r">collect_plots(res_list, k = 4, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-3-1.png" alt="plot of chunk tab-collect-get-signatures-3"/></p>

</div>
<div id='tab-collect-get-signatures-4'>
<pre><code class="r">collect_plots(res_list, k = 5, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-4-1.png" alt="plot of chunk tab-collect-get-signatures-4"/></p>

</div>
<div id='tab-collect-get-signatures-5'>
<pre><code class="r">collect_plots(res_list, k = 6, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-5-1.png" alt="plot of chunk tab-collect-get-signatures-5"/></p>

</div>
</div>



### Statistics table

The statistics used for measuring the stability of consensus partitioning.
([How are they
defined?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13))


<script>
$( function() {
	$( '#tabs-get-stats-from-consensus-partition-list' ).tabs();
} );
</script>
<div id='tabs-get-stats-from-consensus-partition-list'>
<ul>
<li><a href='#tab-get-stats-from-consensus-partition-list-1'>k = 2</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-2'>k = 3</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-3'>k = 4</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-4'>k = 5</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-5'>k = 6</a></li>
</ul>
<div id='tab-get-stats-from-consensus-partition-list-1'>
<pre><code class="r">get_stats(res_list, k = 2)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      2 0.701           0.882       0.946          0.457 0.538   0.538
#&gt; CV:NMF      2 0.910           0.905       0.961          0.398 0.618   0.618
#&gt; MAD:NMF     2 0.737           0.884       0.951          0.505 0.491   0.491
#&gt; ATC:NMF     2 0.633           0.810       0.915          0.476 0.502   0.502
#&gt; SD:skmeans  2 0.687           0.876       0.942          0.464 0.551   0.551
#&gt; CV:skmeans  2 0.960           0.936       0.975          0.406 0.599   0.599
#&gt; MAD:skmeans 2 0.959           0.953       0.980          0.504 0.497   0.497
#&gt; ATC:skmeans 2 1.000           0.992       0.996          0.497 0.502   0.502
#&gt; SD:mclust   2 1.000           1.000       1.000          0.112 0.889   0.889
#&gt; CV:mclust   2 0.962           0.950       0.980          0.291 0.708   0.708
#&gt; MAD:mclust  2 1.000           0.998       0.999          0.114 0.889   0.889
#&gt; ATC:mclust  2 0.743           0.929       0.957          0.291 0.708   0.708
#&gt; SD:kmeans   2 1.000           0.971       0.973          0.135 0.889   0.889
#&gt; CV:kmeans   2 1.000           1.000       1.000          0.238 0.762   0.762
#&gt; MAD:kmeans  2 0.483           0.817       0.836          0.374 0.502   0.502
#&gt; ATC:kmeans  2 1.000           1.000       1.000          0.112 0.889   0.889
#&gt; SD:pam      2 1.000           1.000       1.000          0.112 0.889   0.889
#&gt; CV:pam      2 1.000           0.991       0.996          0.215 0.792   0.792
#&gt; MAD:pam     2 0.705           0.943       0.940          0.157 0.889   0.889
#&gt; ATC:pam     2 1.000           1.000       1.000          0.112 0.889   0.889
#&gt; SD:hclust   2 1.000           1.000       1.000          0.112 0.889   0.889
#&gt; CV:hclust   2 1.000           0.998       0.999          0.238 0.762   0.762
#&gt; MAD:hclust  2 1.000           1.000       1.000          0.112 0.889   0.889
#&gt; ATC:hclust  2 1.000           1.000       1.000          0.112 0.889   0.889
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-2'>
<pre><code class="r">get_stats(res_list, k = 3)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      3 0.450           0.590       0.805         0.4035 0.619   0.394
#&gt; CV:NMF      3 0.466           0.645       0.829         0.5575 0.716   0.549
#&gt; MAD:NMF     3 0.528           0.764       0.867         0.3154 0.718   0.487
#&gt; ATC:NMF     3 0.407           0.633       0.790         0.3014 0.813   0.645
#&gt; SD:skmeans  3 0.889           0.889       0.947         0.4545 0.744   0.546
#&gt; CV:skmeans  3 0.590           0.627       0.776         0.4539 0.673   0.489
#&gt; MAD:skmeans 3 0.790           0.874       0.929         0.3285 0.787   0.592
#&gt; ATC:skmeans 3 0.728           0.487       0.780         0.3102 0.922   0.844
#&gt; SD:mclust   3 0.344           0.664       0.804         2.8877 0.706   0.669
#&gt; CV:mclust   3 0.350           0.316       0.686         0.7175 0.630   0.508
#&gt; MAD:mclust  3 0.322           0.473       0.733         3.3337 0.548   0.491
#&gt; ATC:mclust  3 0.481           0.755       0.879         0.5619 0.882   0.837
#&gt; SD:kmeans   3 0.799           0.908       0.954         2.1147 0.729   0.695
#&gt; CV:kmeans   3 0.448           0.681       0.803         1.1225 0.736   0.654
#&gt; MAD:kmeans  3 0.615           0.803       0.909         0.3684 0.642   0.457
#&gt; ATC:kmeans  3 0.962           0.949       0.980         4.0272 0.549   0.493
#&gt; SD:pam      3 0.635           0.909       0.950         2.7266 0.729   0.695
#&gt; CV:pam      3 0.964           0.882       0.969         0.2477 0.966   0.957
#&gt; MAD:pam     3 0.627           0.844       0.921         1.9545 0.706   0.669
#&gt; ATC:pam     3 1.000           0.986       0.995         3.9513 0.557   0.501
#&gt; SD:hclust   3 0.649           0.872       0.938         2.6062 0.706   0.669
#&gt; CV:hclust   3 1.000           0.979       0.999         0.0259 0.995   0.994
#&gt; MAD:hclust  3 0.429           0.609       0.768         3.2726 0.729   0.695
#&gt; ATC:hclust  3 0.669           0.838       0.921         3.8080 0.563   0.508
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-3'>
<pre><code class="r">get_stats(res_list, k = 4)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      4 0.440           0.594       0.741         0.1449 0.825   0.538
#&gt; CV:NMF      4 0.628           0.625       0.832         0.1428 0.883   0.698
#&gt; MAD:NMF     4 0.576           0.657       0.812         0.1295 0.835   0.551
#&gt; ATC:NMF     4 0.365           0.510       0.730         0.1116 0.865   0.664
#&gt; SD:skmeans  4 0.871           0.809       0.911         0.0887 0.908   0.732
#&gt; CV:skmeans  4 0.539           0.522       0.759         0.1523 0.722   0.425
#&gt; MAD:skmeans 4 0.705           0.787       0.874         0.1113 0.908   0.732
#&gt; ATC:skmeans 4 0.647           0.557       0.722         0.0984 0.744   0.445
#&gt; SD:mclust   4 0.475           0.826       0.849         0.4174 0.767   0.623
#&gt; CV:mclust   4 0.264           0.592       0.736         0.0516 0.623   0.484
#&gt; MAD:mclust  4 0.603           0.790       0.866         0.3488 0.687   0.406
#&gt; ATC:mclust  4 0.570           0.854       0.872         0.4551 0.643   0.444
#&gt; SD:kmeans   4 0.821           0.860       0.933         0.5959 0.701   0.516
#&gt; CV:kmeans   4 0.470           0.638       0.817         0.1765 0.795   0.628
#&gt; MAD:kmeans  4 0.747           0.753       0.893         0.3384 0.677   0.410
#&gt; ATC:kmeans  4 0.678           0.805       0.880         0.2222 0.824   0.618
#&gt; SD:pam      4 0.906           0.890       0.954         0.5386 0.705   0.537
#&gt; CV:pam      4 0.663           0.894       0.944         0.3629 0.905   0.875
#&gt; MAD:pam     4 0.724           0.882       0.929         0.4021 0.753   0.590
#&gt; ATC:pam     4 1.000           0.950       0.983         0.1277 0.926   0.834
#&gt; SD:hclust   4 0.573           0.803       0.880         0.2413 0.984   0.973
#&gt; CV:hclust   4 0.576           0.611       0.869         0.5020 0.967   0.956
#&gt; MAD:hclust  4 0.420           0.652       0.749         0.3494 0.686   0.498
#&gt; ATC:hclust  4 0.569           0.687       0.808         0.1560 1.000   1.000
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-4'>
<pre><code class="r">get_stats(res_list, k = 5)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      5 0.526           0.472       0.724         0.0629 0.921   0.703
#&gt; CV:NMF      5 0.577           0.542       0.712         0.0681 0.943   0.825
#&gt; MAD:NMF     5 0.592           0.563       0.761         0.0598 0.897   0.625
#&gt; ATC:NMF     5 0.388           0.386       0.615         0.0599 0.918   0.762
#&gt; SD:skmeans  5 0.749           0.703       0.852         0.0829 0.888   0.614
#&gt; CV:skmeans  5 0.667           0.685       0.829         0.1119 0.827   0.553
#&gt; MAD:skmeans 5 0.680           0.616       0.792         0.0672 0.917   0.699
#&gt; ATC:skmeans 5 0.679           0.664       0.827         0.0668 0.903   0.652
#&gt; SD:mclust   5 0.528           0.764       0.840         0.0915 0.928   0.833
#&gt; CV:mclust   5 0.345           0.452       0.739         0.1320 0.780   0.673
#&gt; MAD:mclust  5 0.546           0.644       0.779         0.0850 0.955   0.851
#&gt; ATC:mclust  5 0.659           0.504       0.756         0.0430 0.686   0.331
#&gt; SD:kmeans   5 0.657           0.559       0.762         0.1140 0.922   0.764
#&gt; CV:kmeans   5 0.476           0.471       0.714         0.1447 0.905   0.766
#&gt; MAD:kmeans  5 0.619           0.649       0.793         0.1117 0.863   0.597
#&gt; ATC:kmeans  5 0.696           0.694       0.808         0.0798 0.959   0.869
#&gt; SD:pam      5 0.787           0.813       0.911         0.1495 0.894   0.715
#&gt; CV:pam      5 0.488           0.628       0.857         0.3178 0.934   0.901
#&gt; MAD:pam     5 0.808           0.883       0.927         0.1949 0.760   0.421
#&gt; ATC:pam     5 0.918           0.874       0.956         0.2095 0.807   0.523
#&gt; SD:hclust   5 0.571           0.730       0.854         0.3777 0.729   0.531
#&gt; CV:hclust   5 0.468           0.725       0.817         0.1292 1.000   1.000
#&gt; MAD:hclust  5 0.611           0.626       0.782         0.1801 0.843   0.548
#&gt; ATC:hclust  5 0.800           0.825       0.908         0.1423 0.814   0.597
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-5'>
<pre><code class="r">get_stats(res_list, k = 6)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      6 0.593           0.458       0.700         0.0345 0.914   0.650
#&gt; CV:NMF      6 0.630           0.551       0.751         0.0492 0.824   0.466
#&gt; MAD:NMF     6 0.650           0.551       0.747         0.0341 0.931   0.694
#&gt; ATC:NMF     6 0.423           0.375       0.595         0.0781 0.814   0.460
#&gt; SD:skmeans  6 0.798           0.669       0.824         0.0460 0.938   0.710
#&gt; CV:skmeans  6 0.715           0.696       0.794         0.0530 0.926   0.727
#&gt; MAD:skmeans 6 0.719           0.590       0.738         0.0431 0.914   0.626
#&gt; ATC:skmeans 6 0.695           0.546       0.761         0.0402 0.965   0.842
#&gt; SD:mclust   6 0.540           0.667       0.728         0.1486 0.720   0.343
#&gt; CV:mclust   6 0.331           0.409       0.697         0.1467 0.723   0.492
#&gt; MAD:mclust  6 0.581           0.478       0.746         0.0637 0.867   0.556
#&gt; ATC:mclust  6 0.639           0.576       0.779         0.1259 0.783   0.421
#&gt; SD:kmeans   6 0.651           0.508       0.701         0.0593 0.860   0.531
#&gt; CV:kmeans   6 0.477           0.581       0.755         0.0919 0.856   0.584
#&gt; MAD:kmeans  6 0.721           0.626       0.785         0.0587 0.915   0.661
#&gt; ATC:kmeans  6 0.691           0.563       0.764         0.0548 0.961   0.856
#&gt; SD:pam      6 0.807           0.767       0.881         0.1021 0.852   0.516
#&gt; CV:pam      6 0.502           0.432       0.752         0.1338 0.748   0.614
#&gt; MAD:pam     6 0.855           0.853       0.923         0.0425 0.962   0.832
#&gt; ATC:pam     6 0.878           0.842       0.953         0.0190 0.986   0.942
#&gt; SD:hclust   6 0.596           0.632       0.816         0.0826 0.928   0.767
#&gt; CV:hclust   6 0.496           0.695       0.819         0.0470 0.962   0.947
#&gt; MAD:hclust  6 0.660           0.682       0.762         0.0290 0.975   0.887
#&gt; ATC:hclust  6 0.779           0.764       0.885         0.0442 0.987   0.955
</code></pre>

</div>
</div>

Following heatmap plots the partition for each combination of methods and the
lightness correspond to the silhouette scores for samples in each method. On
top the consensus subgroup is inferred from all methods by taking the mean
silhouette scores as weight.


<script>
$( function() {
	$( '#tabs-collect-stats-from-consensus-partition-list' ).tabs();
} );
</script>
<div id='tabs-collect-stats-from-consensus-partition-list'>
<ul>
<li><a href='#tab-collect-stats-from-consensus-partition-list-1'>k = 2</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-2'>k = 3</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-3'>k = 4</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-4'>k = 5</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-5'>k = 6</a></li>
</ul>
<div id='tab-collect-stats-from-consensus-partition-list-1'>
<pre><code class="r">collect_stats(res_list, k = 2)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-1-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-1"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-2'>
<pre><code class="r">collect_stats(res_list, k = 3)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-2-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-2"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-3'>
<pre><code class="r">collect_stats(res_list, k = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-3-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-3"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-4'>
<pre><code class="r">collect_stats(res_list, k = 5)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-4-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-4"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-5'>
<pre><code class="r">collect_stats(res_list, k = 6)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-5-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-5"/></p>

</div>
</div>

### Partition from all methods



Collect partitions from all methods:


<script>
$( function() {
	$( '#tabs-collect-classes-from-consensus-partition-list' ).tabs();
} );
</script>
<div id='tabs-collect-classes-from-consensus-partition-list'>
<ul>
<li><a href='#tab-collect-classes-from-consensus-partition-list-1'>k = 2</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-2'>k = 3</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-3'>k = 4</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-4'>k = 5</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-5'>k = 6</a></li>
</ul>
<div id='tab-collect-classes-from-consensus-partition-list-1'>
<pre><code class="r">collect_classes(res_list, k = 2)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-1-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-1"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-2'>
<pre><code class="r">collect_classes(res_list, k = 3)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-2-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-2"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-3'>
<pre><code class="r">collect_classes(res_list, k = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-3-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-3"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-4'>
<pre><code class="r">collect_classes(res_list, k = 5)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-4-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-4"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-5'>
<pre><code class="r">collect_classes(res_list, k = 6)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-5-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-5"/></p>

</div>
</div>



### Top rows overlap


Overlap of top rows from different top-row methods:


<script>
$( function() {
	$( '#tabs-top-rows-overlap-by-euler' ).tabs();
} );
</script>
<div id='tabs-top-rows-overlap-by-euler'>
<ul>
<li><a href='#tab-top-rows-overlap-by-euler-1'>top_n = 1000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-2'>top_n = 2000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-3'>top_n = 3000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-4'>top_n = 4000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-5'>top_n = 5000</a></li>
</ul>
<div id='tab-top-rows-overlap-by-euler-1'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 1000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-1-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-1"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-2'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 2000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-2-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-2"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-3'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 3000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-3-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-3"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-4'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 4000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-4-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-4"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-5'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 5000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-5-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-5"/></p>

</div>
</div>

Also visualize the correspondance of rankings between different top-row methods:


<script>
$( function() {
	$( '#tabs-top-rows-overlap-by-correspondance' ).tabs();
} );
</script>
<div id='tabs-top-rows-overlap-by-correspondance'>
<ul>
<li><a href='#tab-top-rows-overlap-by-correspondance-1'>top_n = 1000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-2'>top_n = 2000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-3'>top_n = 3000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-4'>top_n = 4000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-5'>top_n = 5000</a></li>
</ul>
<div id='tab-top-rows-overlap-by-correspondance-1'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 1000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-1-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-1"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-2'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 2000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-2-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-2"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-3'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 3000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-3-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-3"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-4'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 4000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-4-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-4"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-5'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 5000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-5-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-5"/></p>

</div>
</div>


Heatmaps of the top rows:



<script>
$( function() {
	$( '#tabs-top-rows-heatmap' ).tabs();
} );
</script>
<div id='tabs-top-rows-heatmap'>
<ul>
<li><a href='#tab-top-rows-heatmap-1'>top_n = 1000</a></li>
<li><a href='#tab-top-rows-heatmap-2'>top_n = 2000</a></li>
<li><a href='#tab-top-rows-heatmap-3'>top_n = 3000</a></li>
<li><a href='#tab-top-rows-heatmap-4'>top_n = 4000</a></li>
<li><a href='#tab-top-rows-heatmap-5'>top_n = 5000</a></li>
</ul>
<div id='tab-top-rows-heatmap-1'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 1000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-1-1.png" alt="plot of chunk tab-top-rows-heatmap-1"/></p>

</div>
<div id='tab-top-rows-heatmap-2'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 2000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-2-1.png" alt="plot of chunk tab-top-rows-heatmap-2"/></p>

</div>
<div id='tab-top-rows-heatmap-3'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 3000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-3-1.png" alt="plot of chunk tab-top-rows-heatmap-3"/></p>

</div>
<div id='tab-top-rows-heatmap-4'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 4000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-4-1.png" alt="plot of chunk tab-top-rows-heatmap-4"/></p>

</div>
<div id='tab-top-rows-heatmap-5'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 5000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-5-1.png" alt="plot of chunk tab-top-rows-heatmap-5"/></p>

</div>
</div>



 
## Results for each method


---------------------------------------------------




### SD:hclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "hclust"]
# you can also extract it by
# res = res_list["SD:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 18140 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-hclust-collect-plots](figure_cola/SD-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-hclust-select-partition-number](figure_cola/SD-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.1117 0.889   0.889
#> 3 3 0.649           0.872       0.938         2.6062 0.706   0.669
#> 4 4 0.573           0.803       0.880         0.2413 0.984   0.973
#> 5 5 0.571           0.730       0.854         0.3777 0.729   0.531
#> 6 6 0.596           0.632       0.816         0.0826 0.928   0.767
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-get-classes'>
<ul>
<li><a href='#tab-SD-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-hclust-get-classes-1'>
<p><a id='tab-SD-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette p1 p2
#&gt; ERR519515     1       0          1  1  0
#&gt; ERR519516     1       0          1  1  0
#&gt; ERR519520     1       0          1  1  0
#&gt; ERR519513     1       0          1  1  0
#&gt; ERR519481     1       0          1  1  0
#&gt; ERR519491     1       0          1  1  0
#&gt; ERR519473     1       0          1  1  0
#&gt; ERR519518     1       0          1  1  0
#&gt; ERR519512     1       0          1  1  0
#&gt; ERR519521     1       0          1  1  0
#&gt; ERR519488     1       0          1  1  0
#&gt; ERR519493     1       0          1  1  0
#&gt; ERR519514     1       0          1  1  0
#&gt; ERR519479     1       0          1  1  0
#&gt; ERR519509     1       0          1  1  0
#&gt; ERR519472     1       0          1  1  0
#&gt; ERR519510     1       0          1  1  0
#&gt; ERR519470     1       0          1  1  0
#&gt; ERR519495     1       0          1  1  0
#&gt; ERR519522     1       0          1  1  0
#&gt; ERR519523     1       0          1  1  0
#&gt; ERR519503     1       0          1  1  0
#&gt; ERR519471     1       0          1  1  0
#&gt; ERR519500     1       0          1  1  0
#&gt; ERR519485     1       0          1  1  0
#&gt; ERR519476     2       0          1  0  1
#&gt; ERR519502     1       0          1  1  0
#&gt; ERR519486     1       0          1  1  0
#&gt; ERR519478     1       0          1  1  0
#&gt; ERR519497     1       0          1  1  0
#&gt; ERR519467     1       0          1  1  0
#&gt; ERR519489     1       0          1  1  0
#&gt; ERR519494     1       0          1  1  0
#&gt; ERR519474     1       0          1  1  0
#&gt; ERR519505     1       0          1  1  0
#&gt; ERR519517     1       0          1  1  0
#&gt; ERR519484     1       0          1  1  0
#&gt; ERR519498     1       0          1  1  0
#&gt; ERR519490     1       0          1  1  0
#&gt; ERR519507     1       0          1  1  0
#&gt; ERR519511     1       0          1  1  0
#&gt; ERR519468     1       0          1  1  0
#&gt; ERR519482     1       0          1  1  0
#&gt; ERR519475     2       0          1  0  1
#&gt; ERR519496     1       0          1  1  0
#&gt; ERR519506     1       0          1  1  0
#&gt; ERR519469     1       0          1  1  0
#&gt; ERR519480     1       0          1  1  0
#&gt; ERR519487     1       0          1  1  0
#&gt; ERR519483     1       0          1  1  0
#&gt; ERR519477     2       0          1  0  1
#&gt; ERR519499     1       0          1  1  0
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-1-a').click(function(){
  $('#tab-SD-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-2'>
<p><a id='tab-SD-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3
#&gt; ERR519515     1  0.0000     0.9334 1.000  0 0.000
#&gt; ERR519516     1  0.0237     0.9333 0.996  0 0.004
#&gt; ERR519520     1  0.0000     0.9334 1.000  0 0.000
#&gt; ERR519513     1  0.3412     0.9013 0.876  0 0.124
#&gt; ERR519481     1  0.3412     0.9002 0.876  0 0.124
#&gt; ERR519491     1  0.0237     0.9333 0.996  0 0.004
#&gt; ERR519473     1  0.3551     0.8962 0.868  0 0.132
#&gt; ERR519518     1  0.2796     0.9136 0.908  0 0.092
#&gt; ERR519512     1  0.0000     0.9334 1.000  0 0.000
#&gt; ERR519521     1  0.0000     0.9334 1.000  0 0.000
#&gt; ERR519488     1  0.0000     0.9334 1.000  0 0.000
#&gt; ERR519493     1  0.0237     0.9333 0.996  0 0.004
#&gt; ERR519514     1  0.0000     0.9334 1.000  0 0.000
#&gt; ERR519479     1  0.3551     0.8962 0.868  0 0.132
#&gt; ERR519509     1  0.0000     0.9334 1.000  0 0.000
#&gt; ERR519472     1  0.3482     0.8993 0.872  0 0.128
#&gt; ERR519510     1  0.3412     0.9002 0.876  0 0.124
#&gt; ERR519470     1  0.0000     0.9334 1.000  0 0.000
#&gt; ERR519495     1  0.2448     0.9196 0.924  0 0.076
#&gt; ERR519522     1  0.0000     0.9334 1.000  0 0.000
#&gt; ERR519523     1  0.0000     0.9334 1.000  0 0.000
#&gt; ERR519503     3  0.6308     0.0642 0.492  0 0.508
#&gt; ERR519471     1  0.0000     0.9334 1.000  0 0.000
#&gt; ERR519500     1  0.0237     0.9333 0.996  0 0.004
#&gt; ERR519485     1  0.0892     0.9288 0.980  0 0.020
#&gt; ERR519476     2  0.0000     1.0000 0.000  1 0.000
#&gt; ERR519502     1  0.3412     0.9002 0.876  0 0.124
#&gt; ERR519486     1  0.0892     0.9288 0.980  0 0.020
#&gt; ERR519478     1  0.0000     0.9334 1.000  0 0.000
#&gt; ERR519497     1  0.2796     0.9136 0.908  0 0.092
#&gt; ERR519467     1  0.0000     0.9334 1.000  0 0.000
#&gt; ERR519489     1  0.0237     0.9333 0.996  0 0.004
#&gt; ERR519494     3  0.1860     0.7376 0.052  0 0.948
#&gt; ERR519474     1  0.0237     0.9333 0.996  0 0.004
#&gt; ERR519505     1  0.3482     0.8992 0.872  0 0.128
#&gt; ERR519517     3  0.0000     0.7629 0.000  0 1.000
#&gt; ERR519484     1  0.4002     0.8701 0.840  0 0.160
#&gt; ERR519498     1  0.3412     0.9013 0.876  0 0.124
#&gt; ERR519490     3  0.0000     0.7629 0.000  0 1.000
#&gt; ERR519507     1  0.3551     0.8962 0.868  0 0.132
#&gt; ERR519511     1  0.3412     0.9002 0.876  0 0.124
#&gt; ERR519468     1  0.3816     0.8829 0.852  0 0.148
#&gt; ERR519482     3  0.0000     0.7629 0.000  0 1.000
#&gt; ERR519475     2  0.0000     1.0000 0.000  1 0.000
#&gt; ERR519496     1  0.0000     0.9334 1.000  0 0.000
#&gt; ERR519506     3  0.5254     0.5787 0.264  0 0.736
#&gt; ERR519469     1  0.3816     0.8829 0.852  0 0.148
#&gt; ERR519480     3  0.0000     0.7629 0.000  0 1.000
#&gt; ERR519487     3  0.0000     0.7629 0.000  0 1.000
#&gt; ERR519483     3  0.5254     0.5787 0.264  0 0.736
#&gt; ERR519477     2  0.0000     1.0000 0.000  1 0.000
#&gt; ERR519499     3  0.0000     0.7629 0.000  0 1.000
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-2-a').click(function(){
  $('#tab-SD-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-3'>
<p><a id='tab-SD-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3    p4
#&gt; ERR519515     1  0.3801      0.723 0.780  0 0.000 0.220
#&gt; ERR519516     1  0.3726      0.732 0.788  0 0.000 0.212
#&gt; ERR519520     1  0.0188      0.820 0.996  0 0.000 0.004
#&gt; ERR519513     1  0.3099      0.805 0.876  0 0.020 0.104
#&gt; ERR519481     1  0.2988      0.803 0.876  0 0.012 0.112
#&gt; ERR519491     1  0.3726      0.732 0.788  0 0.000 0.212
#&gt; ERR519473     1  0.3161      0.801 0.864  0 0.012 0.124
#&gt; ERR519518     1  0.2412      0.813 0.908  0 0.008 0.084
#&gt; ERR519512     1  0.0188      0.820 0.996  0 0.000 0.004
#&gt; ERR519521     1  0.0000      0.820 1.000  0 0.000 0.000
#&gt; ERR519488     1  0.4193      0.658 0.732  0 0.000 0.268
#&gt; ERR519493     1  0.3726      0.732 0.788  0 0.000 0.212
#&gt; ERR519514     1  0.3801      0.723 0.780  0 0.000 0.220
#&gt; ERR519479     1  0.3161      0.801 0.864  0 0.012 0.124
#&gt; ERR519509     1  0.4193      0.658 0.732  0 0.000 0.268
#&gt; ERR519472     1  0.3105      0.804 0.868  0 0.012 0.120
#&gt; ERR519510     1  0.2988      0.803 0.876  0 0.012 0.112
#&gt; ERR519470     1  0.3801      0.723 0.780  0 0.000 0.220
#&gt; ERR519495     1  0.2675      0.821 0.892  0 0.008 0.100
#&gt; ERR519522     1  0.1474      0.812 0.948  0 0.000 0.052
#&gt; ERR519523     1  0.0336      0.820 0.992  0 0.000 0.008
#&gt; ERR519503     4  0.4542      0.569 0.228  0 0.020 0.752
#&gt; ERR519471     1  0.3801      0.723 0.780  0 0.000 0.220
#&gt; ERR519500     1  0.1118      0.817 0.964  0 0.000 0.036
#&gt; ERR519485     1  0.4088      0.717 0.764  0 0.004 0.232
#&gt; ERR519476     2  0.0000      1.000 0.000  1 0.000 0.000
#&gt; ERR519502     1  0.2988      0.803 0.876  0 0.012 0.112
#&gt; ERR519486     1  0.4088      0.717 0.764  0 0.004 0.232
#&gt; ERR519478     1  0.3801      0.723 0.780  0 0.000 0.220
#&gt; ERR519497     1  0.2412      0.813 0.908  0 0.008 0.084
#&gt; ERR519467     1  0.1474      0.812 0.948  0 0.000 0.052
#&gt; ERR519489     1  0.1118      0.817 0.964  0 0.000 0.036
#&gt; ERR519494     3  0.4127      0.711 0.052  0 0.824 0.124
#&gt; ERR519474     1  0.1389      0.816 0.952  0 0.000 0.048
#&gt; ERR519505     1  0.3160      0.804 0.872  0 0.020 0.108
#&gt; ERR519517     3  0.0000      0.956 0.000  0 1.000 0.000
#&gt; ERR519484     1  0.3787      0.778 0.840  0 0.036 0.124
#&gt; ERR519498     1  0.3099      0.805 0.876  0 0.020 0.104
#&gt; ERR519490     3  0.0000      0.956 0.000  0 1.000 0.000
#&gt; ERR519507     1  0.3161      0.801 0.864  0 0.012 0.124
#&gt; ERR519511     1  0.2988      0.803 0.876  0 0.012 0.112
#&gt; ERR519468     1  0.3542      0.791 0.852  0 0.028 0.120
#&gt; ERR519482     3  0.0000      0.956 0.000  0 1.000 0.000
#&gt; ERR519475     2  0.0000      1.000 0.000  1 0.000 0.000
#&gt; ERR519496     1  0.3801      0.723 0.780  0 0.000 0.220
#&gt; ERR519506     4  0.0707      0.737 0.000  0 0.020 0.980
#&gt; ERR519469     1  0.3497      0.791 0.852  0 0.024 0.124
#&gt; ERR519480     3  0.0000      0.956 0.000  0 1.000 0.000
#&gt; ERR519487     3  0.0000      0.956 0.000  0 1.000 0.000
#&gt; ERR519483     4  0.0707      0.737 0.000  0 0.020 0.980
#&gt; ERR519477     2  0.0000      1.000 0.000  1 0.000 0.000
#&gt; ERR519499     3  0.0000      0.956 0.000  0 1.000 0.000
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-3-a').click(function(){
  $('#tab-SD-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-4'>
<p><a id='tab-SD-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3    p4    p5
#&gt; ERR519515     1  0.1043      0.813 0.960  0 0.000 0.040 0.000
#&gt; ERR519516     1  0.3242      0.756 0.784  0 0.000 0.216 0.000
#&gt; ERR519520     4  0.4689      0.203 0.424  0 0.000 0.560 0.016
#&gt; ERR519513     4  0.3274      0.670 0.000  0 0.000 0.780 0.220
#&gt; ERR519481     4  0.0794      0.776 0.028  0 0.000 0.972 0.000
#&gt; ERR519491     1  0.3242      0.756 0.784  0 0.000 0.216 0.000
#&gt; ERR519473     4  0.0955      0.775 0.028  0 0.000 0.968 0.004
#&gt; ERR519518     4  0.1626      0.773 0.044  0 0.000 0.940 0.016
#&gt; ERR519512     4  0.4689      0.203 0.424  0 0.000 0.560 0.016
#&gt; ERR519521     4  0.2966      0.717 0.136  0 0.000 0.848 0.016
#&gt; ERR519488     1  0.0609      0.738 0.980  0 0.000 0.000 0.020
#&gt; ERR519493     1  0.3242      0.756 0.784  0 0.000 0.216 0.000
#&gt; ERR519514     1  0.1043      0.813 0.960  0 0.000 0.040 0.000
#&gt; ERR519479     4  0.1892      0.765 0.080  0 0.000 0.916 0.004
#&gt; ERR519509     1  0.0609      0.738 0.980  0 0.000 0.000 0.020
#&gt; ERR519472     4  0.1041      0.775 0.032  0 0.000 0.964 0.004
#&gt; ERR519510     4  0.2761      0.752 0.024  0 0.000 0.872 0.104
#&gt; ERR519470     1  0.1043      0.813 0.960  0 0.000 0.040 0.000
#&gt; ERR519495     4  0.3231      0.678 0.196  0 0.000 0.800 0.004
#&gt; ERR519522     1  0.3421      0.703 0.788  0 0.000 0.204 0.008
#&gt; ERR519523     4  0.4696      0.190 0.428  0 0.000 0.556 0.016
#&gt; ERR519503     5  0.4256      0.590 0.436  0 0.000 0.000 0.564
#&gt; ERR519471     1  0.1043      0.813 0.960  0 0.000 0.040 0.000
#&gt; ERR519500     4  0.4138      0.335 0.384  0 0.000 0.616 0.000
#&gt; ERR519485     1  0.3710      0.762 0.784  0 0.000 0.192 0.024
#&gt; ERR519476     2  0.0000      1.000 0.000  1 0.000 0.000 0.000
#&gt; ERR519502     4  0.0794      0.776 0.028  0 0.000 0.972 0.000
#&gt; ERR519486     1  0.3710      0.762 0.784  0 0.000 0.192 0.024
#&gt; ERR519478     1  0.1205      0.812 0.956  0 0.000 0.040 0.004
#&gt; ERR519497     4  0.2054      0.775 0.052  0 0.000 0.920 0.028
#&gt; ERR519467     1  0.3642      0.682 0.760  0 0.000 0.232 0.008
#&gt; ERR519489     4  0.4060      0.382 0.360  0 0.000 0.640 0.000
#&gt; ERR519494     3  0.3282      0.694 0.000  0 0.804 0.188 0.008
#&gt; ERR519474     4  0.4171      0.309 0.396  0 0.000 0.604 0.000
#&gt; ERR519505     4  0.4210      0.650 0.036  0 0.000 0.740 0.224
#&gt; ERR519517     3  0.0000      0.952 0.000  0 1.000 0.000 0.000
#&gt; ERR519484     4  0.2959      0.736 0.008  0 0.016 0.864 0.112
#&gt; ERR519498     4  0.2006      0.765 0.012  0 0.000 0.916 0.072
#&gt; ERR519490     3  0.0000      0.952 0.000  0 1.000 0.000 0.000
#&gt; ERR519507     4  0.1892      0.765 0.080  0 0.000 0.916 0.004
#&gt; ERR519511     4  0.2761      0.752 0.024  0 0.000 0.872 0.104
#&gt; ERR519468     4  0.3455      0.665 0.000  0 0.008 0.784 0.208
#&gt; ERR519482     3  0.0000      0.952 0.000  0 1.000 0.000 0.000
#&gt; ERR519475     2  0.0000      1.000 0.000  1 0.000 0.000 0.000
#&gt; ERR519496     1  0.2127      0.805 0.892  0 0.000 0.108 0.000
#&gt; ERR519506     5  0.3789      0.794 0.212  0 0.000 0.020 0.768
#&gt; ERR519469     4  0.3333      0.666 0.000  0 0.004 0.788 0.208
#&gt; ERR519480     3  0.0162      0.949 0.000  0 0.996 0.000 0.004
#&gt; ERR519487     3  0.0000      0.952 0.000  0 1.000 0.000 0.000
#&gt; ERR519483     5  0.3789      0.794 0.212  0 0.000 0.020 0.768
#&gt; ERR519477     2  0.0000      1.000 0.000  1 0.000 0.000 0.000
#&gt; ERR519499     3  0.0000      0.952 0.000  0 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-4-a').click(function(){
  $('#tab-SD-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-5'>
<p><a id='tab-SD-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3    p4    p5    p6
#&gt; ERR519515     1  0.1141     0.8091 0.948  0 0.000 0.000 0.052 0.000
#&gt; ERR519516     1  0.4088     0.6595 0.668  0 0.000 0.020 0.308 0.004
#&gt; ERR519520     5  0.4332     0.3940 0.288  0 0.000 0.048 0.664 0.000
#&gt; ERR519513     4  0.1327     0.6226 0.000  0 0.000 0.936 0.064 0.000
#&gt; ERR519481     5  0.2092     0.5696 0.000  0 0.000 0.124 0.876 0.000
#&gt; ERR519491     1  0.4053     0.6683 0.676  0 0.000 0.020 0.300 0.004
#&gt; ERR519473     5  0.2288     0.5825 0.004  0 0.000 0.116 0.876 0.004
#&gt; ERR519518     5  0.2178     0.5804 0.000  0 0.000 0.132 0.868 0.000
#&gt; ERR519512     5  0.4332     0.3940 0.288  0 0.000 0.048 0.664 0.000
#&gt; ERR519521     5  0.1141     0.5638 0.000  0 0.000 0.052 0.948 0.000
#&gt; ERR519488     1  0.0260     0.7471 0.992  0 0.000 0.000 0.000 0.008
#&gt; ERR519493     1  0.4053     0.6683 0.676  0 0.000 0.020 0.300 0.004
#&gt; ERR519514     1  0.1141     0.8091 0.948  0 0.000 0.000 0.052 0.000
#&gt; ERR519479     5  0.3557     0.5919 0.056  0 0.000 0.140 0.800 0.004
#&gt; ERR519509     1  0.0260     0.7471 0.992  0 0.000 0.000 0.000 0.008
#&gt; ERR519472     5  0.2355     0.5855 0.008  0 0.000 0.112 0.876 0.004
#&gt; ERR519510     5  0.3817     0.0234 0.000  0 0.000 0.432 0.568 0.000
#&gt; ERR519470     1  0.1141     0.8091 0.948  0 0.000 0.000 0.052 0.000
#&gt; ERR519495     5  0.4497     0.5529 0.184  0 0.000 0.100 0.712 0.004
#&gt; ERR519522     1  0.3161     0.6927 0.776  0 0.000 0.000 0.216 0.008
#&gt; ERR519523     5  0.4291     0.3882 0.292  0 0.000 0.044 0.664 0.000
#&gt; ERR519503     6  0.3838     0.2680 0.448  0 0.000 0.000 0.000 0.552
#&gt; ERR519471     1  0.1141     0.8091 0.948  0 0.000 0.000 0.052 0.000
#&gt; ERR519500     5  0.3724     0.4407 0.268  0 0.000 0.012 0.716 0.004
#&gt; ERR519485     1  0.3922     0.7581 0.772  0 0.000 0.028 0.172 0.028
#&gt; ERR519476     2  0.0000     1.0000 0.000  1 0.000 0.000 0.000 0.000
#&gt; ERR519502     5  0.2092     0.5696 0.000  0 0.000 0.124 0.876 0.000
#&gt; ERR519486     1  0.3922     0.7581 0.772  0 0.000 0.028 0.172 0.028
#&gt; ERR519478     1  0.1285     0.8082 0.944  0 0.000 0.000 0.052 0.004
#&gt; ERR519497     5  0.2491     0.5700 0.000  0 0.000 0.164 0.836 0.000
#&gt; ERR519467     1  0.3804     0.5725 0.656  0 0.000 0.000 0.336 0.008
#&gt; ERR519489     5  0.3584     0.4736 0.244  0 0.000 0.012 0.740 0.004
#&gt; ERR519494     3  0.3506     0.7004 0.000  0 0.792 0.156 0.052 0.000
#&gt; ERR519474     5  0.3788     0.4182 0.280  0 0.000 0.012 0.704 0.004
#&gt; ERR519505     4  0.0547     0.5745 0.000  0 0.000 0.980 0.020 0.000
#&gt; ERR519517     3  0.0000     0.9502 0.000  0 1.000 0.000 0.000 0.000
#&gt; ERR519484     5  0.3995    -0.1228 0.000  0 0.004 0.480 0.516 0.000
#&gt; ERR519498     4  0.3151     0.5068 0.000  0 0.000 0.748 0.252 0.000
#&gt; ERR519490     3  0.0363     0.9475 0.000  0 0.988 0.012 0.000 0.000
#&gt; ERR519507     5  0.3557     0.5919 0.056  0 0.000 0.140 0.800 0.004
#&gt; ERR519511     5  0.3817     0.0234 0.000  0 0.000 0.432 0.568 0.000
#&gt; ERR519468     4  0.4062     0.4680 0.000  0 0.008 0.552 0.440 0.000
#&gt; ERR519482     3  0.0363     0.9475 0.000  0 0.988 0.012 0.000 0.000
#&gt; ERR519475     2  0.0000     1.0000 0.000  1 0.000 0.000 0.000 0.000
#&gt; ERR519496     1  0.2383     0.7968 0.880  0 0.000 0.024 0.096 0.000
#&gt; ERR519506     6  0.0508     0.6382 0.012  0 0.000 0.004 0.000 0.984
#&gt; ERR519469     4  0.3961     0.4668 0.000  0 0.004 0.556 0.440 0.000
#&gt; ERR519480     3  0.0146     0.9485 0.000  0 0.996 0.000 0.000 0.004
#&gt; ERR519487     3  0.0000     0.9502 0.000  0 1.000 0.000 0.000 0.000
#&gt; ERR519483     6  0.0363     0.6390 0.012  0 0.000 0.000 0.000 0.988
#&gt; ERR519477     2  0.0000     1.0000 0.000  1 0.000 0.000 0.000 0.000
#&gt; ERR519499     3  0.0000     0.9502 0.000  0 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-5-a').click(function(){
  $('#tab-SD-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-SD-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-get-signatures'>
<ul>
<li><a href='#tab-SD-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-1-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-1"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-2-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-2"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-3-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-3"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-4-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-4"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-5-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-hclust-signature_compare](figure_cola/SD-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-SD-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-hclust-collect-classes](figure_cola/SD-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:kmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "kmeans"]
# you can also extract it by
# res = res_list["SD:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 18140 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-kmeans-collect-plots](figure_cola/SD-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-kmeans-select-partition-number](figure_cola/SD-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.971       0.973         0.1353 0.889   0.889
#> 3 3 0.799           0.908       0.954         2.1147 0.729   0.695
#> 4 4 0.821           0.860       0.933         0.5959 0.701   0.516
#> 5 5 0.657           0.559       0.762         0.1140 0.922   0.764
#> 6 6 0.651           0.508       0.701         0.0593 0.860   0.531
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-get-classes'>
<ul>
<li><a href='#tab-SD-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-kmeans-get-classes-1'>
<p><a id='tab-SD-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; ERR519515     1  0.1184      0.971 0.984 0.016
#&gt; ERR519516     1  0.0000      0.974 1.000 0.000
#&gt; ERR519520     1  0.0000      0.974 1.000 0.000
#&gt; ERR519513     1  0.3114      0.960 0.944 0.056
#&gt; ERR519481     1  0.2423      0.967 0.960 0.040
#&gt; ERR519491     1  0.1184      0.971 0.984 0.016
#&gt; ERR519473     1  0.2423      0.967 0.960 0.040
#&gt; ERR519518     1  0.3114      0.960 0.944 0.056
#&gt; ERR519512     1  0.0000      0.974 1.000 0.000
#&gt; ERR519521     1  0.2423      0.967 0.960 0.040
#&gt; ERR519488     1  0.1184      0.971 0.984 0.016
#&gt; ERR519493     1  0.0938      0.972 0.988 0.012
#&gt; ERR519514     1  0.1184      0.971 0.984 0.016
#&gt; ERR519479     1  0.0376      0.974 0.996 0.004
#&gt; ERR519509     1  0.1184      0.971 0.984 0.016
#&gt; ERR519472     1  0.0000      0.974 1.000 0.000
#&gt; ERR519510     1  0.1633      0.971 0.976 0.024
#&gt; ERR519470     1  0.1184      0.971 0.984 0.016
#&gt; ERR519495     1  0.1184      0.971 0.984 0.016
#&gt; ERR519522     1  0.1184      0.971 0.984 0.016
#&gt; ERR519523     1  0.0000      0.974 1.000 0.000
#&gt; ERR519503     1  0.1184      0.971 0.984 0.016
#&gt; ERR519471     1  0.1184      0.971 0.984 0.016
#&gt; ERR519500     1  0.0000      0.974 1.000 0.000
#&gt; ERR519485     1  0.1184      0.971 0.984 0.016
#&gt; ERR519476     2  0.3114      1.000 0.056 0.944
#&gt; ERR519502     1  0.2423      0.967 0.960 0.040
#&gt; ERR519486     1  0.1184      0.971 0.984 0.016
#&gt; ERR519478     1  0.1184      0.971 0.984 0.016
#&gt; ERR519497     1  0.2423      0.967 0.960 0.040
#&gt; ERR519467     1  0.1184      0.971 0.984 0.016
#&gt; ERR519489     1  0.0000      0.974 1.000 0.000
#&gt; ERR519494     1  0.3114      0.960 0.944 0.056
#&gt; ERR519474     1  0.0000      0.974 1.000 0.000
#&gt; ERR519505     1  0.1633      0.971 0.976 0.024
#&gt; ERR519517     1  0.3114      0.960 0.944 0.056
#&gt; ERR519484     1  0.2423      0.967 0.960 0.040
#&gt; ERR519498     1  0.2423      0.967 0.960 0.040
#&gt; ERR519490     1  0.3114      0.960 0.944 0.056
#&gt; ERR519507     1  0.0376      0.974 0.996 0.004
#&gt; ERR519511     1  0.1633      0.971 0.976 0.024
#&gt; ERR519468     1  0.3114      0.960 0.944 0.056
#&gt; ERR519482     1  0.3114      0.960 0.944 0.056
#&gt; ERR519475     2  0.3114      1.000 0.056 0.944
#&gt; ERR519496     1  0.1184      0.971 0.984 0.016
#&gt; ERR519506     1  0.1184      0.971 0.984 0.016
#&gt; ERR519469     1  0.2423      0.967 0.960 0.040
#&gt; ERR519480     1  0.3114      0.960 0.944 0.056
#&gt; ERR519487     1  0.3114      0.960 0.944 0.056
#&gt; ERR519483     1  0.1184      0.971 0.984 0.016
#&gt; ERR519477     2  0.3114      1.000 0.056 0.944
#&gt; ERR519499     1  0.3114      0.960 0.944 0.056
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-1-a').click(function(){
  $('#tab-SD-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-2'>
<p><a id='tab-SD-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; ERR519515     1  0.0000      0.935 1.000 0.000 0.000
#&gt; ERR519516     1  0.0000      0.935 1.000 0.000 0.000
#&gt; ERR519520     1  0.0000      0.935 1.000 0.000 0.000
#&gt; ERR519513     3  0.0424      1.000 0.008 0.000 0.992
#&gt; ERR519481     1  0.5216      0.707 0.740 0.000 0.260
#&gt; ERR519491     1  0.0000      0.935 1.000 0.000 0.000
#&gt; ERR519473     1  0.5216      0.707 0.740 0.000 0.260
#&gt; ERR519518     1  0.6154      0.429 0.592 0.000 0.408
#&gt; ERR519512     1  0.0000      0.935 1.000 0.000 0.000
#&gt; ERR519521     1  0.0747      0.926 0.984 0.000 0.016
#&gt; ERR519488     1  0.0000      0.935 1.000 0.000 0.000
#&gt; ERR519493     1  0.0000      0.935 1.000 0.000 0.000
#&gt; ERR519514     1  0.0000      0.935 1.000 0.000 0.000
#&gt; ERR519479     1  0.0000      0.935 1.000 0.000 0.000
#&gt; ERR519509     1  0.0000      0.935 1.000 0.000 0.000
#&gt; ERR519472     1  0.0000      0.935 1.000 0.000 0.000
#&gt; ERR519510     1  0.0747      0.926 0.984 0.000 0.016
#&gt; ERR519470     1  0.0000      0.935 1.000 0.000 0.000
#&gt; ERR519495     1  0.0000      0.935 1.000 0.000 0.000
#&gt; ERR519522     1  0.0000      0.935 1.000 0.000 0.000
#&gt; ERR519523     1  0.0000      0.935 1.000 0.000 0.000
#&gt; ERR519503     1  0.0000      0.935 1.000 0.000 0.000
#&gt; ERR519471     1  0.0000      0.935 1.000 0.000 0.000
#&gt; ERR519500     1  0.0000      0.935 1.000 0.000 0.000
#&gt; ERR519485     1  0.0000      0.935 1.000 0.000 0.000
#&gt; ERR519476     2  0.0424      0.996 0.000 0.992 0.008
#&gt; ERR519502     1  0.5216      0.707 0.740 0.000 0.260
#&gt; ERR519486     1  0.0000      0.935 1.000 0.000 0.000
#&gt; ERR519478     1  0.0000      0.935 1.000 0.000 0.000
#&gt; ERR519497     1  0.5178      0.712 0.744 0.000 0.256
#&gt; ERR519467     1  0.0000      0.935 1.000 0.000 0.000
#&gt; ERR519489     1  0.0000      0.935 1.000 0.000 0.000
#&gt; ERR519494     3  0.0424      1.000 0.008 0.000 0.992
#&gt; ERR519474     1  0.0000      0.935 1.000 0.000 0.000
#&gt; ERR519505     1  0.5178      0.712 0.744 0.000 0.256
#&gt; ERR519517     3  0.0424      1.000 0.008 0.000 0.992
#&gt; ERR519484     1  0.5363      0.684 0.724 0.000 0.276
#&gt; ERR519498     1  0.5216      0.707 0.740 0.000 0.260
#&gt; ERR519490     3  0.0424      1.000 0.008 0.000 0.992
#&gt; ERR519507     1  0.0000      0.935 1.000 0.000 0.000
#&gt; ERR519511     1  0.1964      0.898 0.944 0.000 0.056
#&gt; ERR519468     3  0.0424      1.000 0.008 0.000 0.992
#&gt; ERR519482     3  0.0424      1.000 0.008 0.000 0.992
#&gt; ERR519475     2  0.0000      0.998 0.000 1.000 0.000
#&gt; ERR519496     1  0.0000      0.935 1.000 0.000 0.000
#&gt; ERR519506     1  0.0000      0.935 1.000 0.000 0.000
#&gt; ERR519469     1  0.0000      0.935 1.000 0.000 0.000
#&gt; ERR519480     3  0.0424      1.000 0.008 0.000 0.992
#&gt; ERR519487     3  0.0424      1.000 0.008 0.000 0.992
#&gt; ERR519483     1  0.0000      0.935 1.000 0.000 0.000
#&gt; ERR519477     2  0.0000      0.998 0.000 1.000 0.000
#&gt; ERR519499     3  0.0424      1.000 0.008 0.000 0.992
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-2-a').click(function(){
  $('#tab-SD-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-3'>
<p><a id='tab-SD-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; ERR519515     1  0.0592      0.909 0.984 0.000 0.000 0.016
#&gt; ERR519516     4  0.5000     -0.153 0.496 0.000 0.000 0.504
#&gt; ERR519520     4  0.3444      0.756 0.184 0.000 0.000 0.816
#&gt; ERR519513     3  0.4343      0.560 0.004 0.000 0.732 0.264
#&gt; ERR519481     4  0.0927      0.910 0.008 0.000 0.016 0.976
#&gt; ERR519491     1  0.0707      0.908 0.980 0.000 0.000 0.020
#&gt; ERR519473     4  0.1209      0.910 0.032 0.000 0.004 0.964
#&gt; ERR519518     4  0.1557      0.884 0.000 0.000 0.056 0.944
#&gt; ERR519512     4  0.1557      0.891 0.056 0.000 0.000 0.944
#&gt; ERR519521     4  0.0469      0.910 0.012 0.000 0.000 0.988
#&gt; ERR519488     1  0.1302      0.905 0.956 0.000 0.000 0.044
#&gt; ERR519493     1  0.4790      0.416 0.620 0.000 0.000 0.380
#&gt; ERR519514     1  0.0592      0.909 0.984 0.000 0.000 0.016
#&gt; ERR519479     4  0.1211      0.910 0.040 0.000 0.000 0.960
#&gt; ERR519509     1  0.1302      0.905 0.956 0.000 0.000 0.044
#&gt; ERR519472     4  0.1389      0.908 0.048 0.000 0.000 0.952
#&gt; ERR519510     4  0.1022      0.913 0.032 0.000 0.000 0.968
#&gt; ERR519470     1  0.0592      0.909 0.984 0.000 0.000 0.016
#&gt; ERR519495     4  0.4746      0.462 0.368 0.000 0.000 0.632
#&gt; ERR519522     1  0.1302      0.905 0.956 0.000 0.000 0.044
#&gt; ERR519523     4  0.2216      0.861 0.092 0.000 0.000 0.908
#&gt; ERR519503     1  0.1022      0.898 0.968 0.000 0.000 0.032
#&gt; ERR519471     1  0.0592      0.909 0.984 0.000 0.000 0.016
#&gt; ERR519500     4  0.0921      0.907 0.028 0.000 0.000 0.972
#&gt; ERR519485     1  0.0592      0.907 0.984 0.000 0.000 0.016
#&gt; ERR519476     2  0.0564      0.994 0.004 0.988 0.004 0.004
#&gt; ERR519502     4  0.0779      0.909 0.004 0.000 0.016 0.980
#&gt; ERR519486     1  0.2081      0.865 0.916 0.000 0.000 0.084
#&gt; ERR519478     1  0.1302      0.905 0.956 0.000 0.000 0.044
#&gt; ERR519497     4  0.1042      0.907 0.008 0.000 0.020 0.972
#&gt; ERR519467     1  0.1302      0.905 0.956 0.000 0.000 0.044
#&gt; ERR519489     4  0.1022      0.905 0.032 0.000 0.000 0.968
#&gt; ERR519494     3  0.0188      0.947 0.000 0.000 0.996 0.004
#&gt; ERR519474     1  0.4103      0.694 0.744 0.000 0.000 0.256
#&gt; ERR519505     4  0.1174      0.899 0.012 0.000 0.020 0.968
#&gt; ERR519517     3  0.0336      0.947 0.000 0.000 0.992 0.008
#&gt; ERR519484     4  0.1406      0.908 0.024 0.000 0.016 0.960
#&gt; ERR519498     4  0.0895      0.904 0.004 0.000 0.020 0.976
#&gt; ERR519490     3  0.0188      0.947 0.000 0.000 0.996 0.004
#&gt; ERR519507     4  0.1211      0.910 0.040 0.000 0.000 0.960
#&gt; ERR519511     4  0.0817      0.913 0.024 0.000 0.000 0.976
#&gt; ERR519468     3  0.0336      0.947 0.000 0.000 0.992 0.008
#&gt; ERR519482     3  0.0188      0.947 0.000 0.000 0.996 0.004
#&gt; ERR519475     2  0.0000      0.997 0.000 1.000 0.000 0.000
#&gt; ERR519496     1  0.0592      0.909 0.984 0.000 0.000 0.016
#&gt; ERR519506     1  0.3172      0.793 0.840 0.000 0.000 0.160
#&gt; ERR519469     4  0.1389      0.908 0.048 0.000 0.000 0.952
#&gt; ERR519480     3  0.0188      0.947 0.000 0.000 0.996 0.004
#&gt; ERR519487     3  0.0336      0.947 0.000 0.000 0.992 0.008
#&gt; ERR519483     1  0.3123      0.797 0.844 0.000 0.000 0.156
#&gt; ERR519477     2  0.0000      0.997 0.000 1.000 0.000 0.000
#&gt; ERR519499     3  0.0336      0.947 0.000 0.000 0.992 0.008
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-3-a').click(function(){
  $('#tab-SD-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-4'>
<p><a id='tab-SD-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; ERR519515     1  0.1197      0.712 0.952 0.000 0.000 0.000 0.048
#&gt; ERR519516     1  0.6725     -0.359 0.400 0.000 0.000 0.344 0.256
#&gt; ERR519520     4  0.4618      0.465 0.208 0.000 0.000 0.724 0.068
#&gt; ERR519513     3  0.6549      0.209 0.000 0.000 0.436 0.360 0.204
#&gt; ERR519481     4  0.2127      0.635 0.000 0.000 0.000 0.892 0.108
#&gt; ERR519491     1  0.4165      0.397 0.672 0.000 0.000 0.008 0.320
#&gt; ERR519473     4  0.4201      0.357 0.000 0.000 0.000 0.592 0.408
#&gt; ERR519518     4  0.1300      0.627 0.000 0.000 0.028 0.956 0.016
#&gt; ERR519512     4  0.3532      0.585 0.092 0.000 0.000 0.832 0.076
#&gt; ERR519521     4  0.1671      0.628 0.000 0.000 0.000 0.924 0.076
#&gt; ERR519488     1  0.0000      0.707 1.000 0.000 0.000 0.000 0.000
#&gt; ERR519493     1  0.5956     -0.289 0.476 0.000 0.000 0.108 0.416
#&gt; ERR519514     1  0.1197      0.712 0.952 0.000 0.000 0.000 0.048
#&gt; ERR519479     4  0.4283      0.285 0.000 0.000 0.000 0.544 0.456
#&gt; ERR519509     1  0.0000      0.707 1.000 0.000 0.000 0.000 0.000
#&gt; ERR519472     4  0.4383      0.335 0.004 0.000 0.000 0.572 0.424
#&gt; ERR519510     4  0.3561      0.555 0.000 0.000 0.000 0.740 0.260
#&gt; ERR519470     1  0.1121      0.712 0.956 0.000 0.000 0.000 0.044
#&gt; ERR519495     5  0.5896     -0.164 0.100 0.000 0.000 0.448 0.452
#&gt; ERR519522     1  0.1341      0.683 0.944 0.000 0.000 0.000 0.056
#&gt; ERR519523     4  0.4216      0.552 0.100 0.000 0.000 0.780 0.120
#&gt; ERR519503     1  0.2852      0.560 0.828 0.000 0.000 0.000 0.172
#&gt; ERR519471     1  0.1270      0.710 0.948 0.000 0.000 0.000 0.052
#&gt; ERR519500     4  0.4184      0.533 0.016 0.000 0.000 0.700 0.284
#&gt; ERR519485     1  0.4114      0.272 0.624 0.000 0.000 0.000 0.376
#&gt; ERR519476     2  0.1121      0.976 0.000 0.956 0.000 0.000 0.044
#&gt; ERR519502     4  0.0880      0.641 0.000 0.000 0.000 0.968 0.032
#&gt; ERR519486     1  0.4620      0.166 0.592 0.000 0.000 0.016 0.392
#&gt; ERR519478     1  0.0290      0.707 0.992 0.000 0.000 0.000 0.008
#&gt; ERR519497     4  0.1041      0.633 0.000 0.000 0.004 0.964 0.032
#&gt; ERR519467     1  0.1764      0.675 0.928 0.000 0.000 0.008 0.064
#&gt; ERR519489     4  0.4109      0.531 0.012 0.000 0.000 0.700 0.288
#&gt; ERR519494     3  0.0807      0.890 0.000 0.000 0.976 0.012 0.012
#&gt; ERR519474     5  0.6154      0.491 0.348 0.000 0.000 0.144 0.508
#&gt; ERR519505     4  0.4590      0.303 0.000 0.000 0.012 0.568 0.420
#&gt; ERR519517     3  0.1121      0.890 0.000 0.000 0.956 0.000 0.044
#&gt; ERR519484     4  0.4242      0.406 0.000 0.000 0.000 0.572 0.428
#&gt; ERR519498     4  0.3563      0.528 0.000 0.000 0.012 0.780 0.208
#&gt; ERR519490     3  0.0807      0.890 0.000 0.000 0.976 0.012 0.012
#&gt; ERR519507     4  0.4291      0.263 0.000 0.000 0.000 0.536 0.464
#&gt; ERR519511     4  0.3480      0.584 0.000 0.000 0.000 0.752 0.248
#&gt; ERR519468     3  0.0798      0.891 0.000 0.000 0.976 0.008 0.016
#&gt; ERR519482     3  0.0807      0.890 0.000 0.000 0.976 0.012 0.012
#&gt; ERR519475     2  0.0000      0.988 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519496     1  0.3684      0.467 0.720 0.000 0.000 0.000 0.280
#&gt; ERR519506     5  0.4644      0.575 0.280 0.000 0.000 0.040 0.680
#&gt; ERR519469     4  0.4227      0.342 0.000 0.000 0.000 0.580 0.420
#&gt; ERR519480     3  0.1121      0.887 0.000 0.000 0.956 0.000 0.044
#&gt; ERR519487     3  0.1121      0.890 0.000 0.000 0.956 0.000 0.044
#&gt; ERR519483     5  0.4644      0.575 0.280 0.000 0.000 0.040 0.680
#&gt; ERR519477     2  0.0000      0.988 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519499     3  0.1121      0.890 0.000 0.000 0.956 0.000 0.044
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-4-a').click(function(){
  $('#tab-SD-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-5'>
<p><a id='tab-SD-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; ERR519515     1  0.1141     0.7254 0.948 0.000 0.000 0.000 0.052 0.000
#&gt; ERR519516     1  0.6419    -0.1794 0.340 0.000 0.000 0.324 0.324 0.012
#&gt; ERR519520     4  0.3036     0.4210 0.124 0.000 0.000 0.840 0.008 0.028
#&gt; ERR519513     6  0.5784     0.4176 0.000 0.000 0.236 0.168 0.020 0.576
#&gt; ERR519481     4  0.4963     0.4464 0.000 0.000 0.000 0.612 0.288 0.100
#&gt; ERR519491     1  0.4499     0.4741 0.620 0.000 0.000 0.012 0.344 0.024
#&gt; ERR519473     5  0.3819     0.3358 0.000 0.000 0.000 0.340 0.652 0.008
#&gt; ERR519518     4  0.4403     0.3510 0.000 0.000 0.000 0.708 0.096 0.196
#&gt; ERR519512     4  0.1788     0.5362 0.040 0.000 0.000 0.928 0.028 0.004
#&gt; ERR519521     4  0.0000     0.5225 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; ERR519488     1  0.1075     0.7119 0.952 0.000 0.000 0.000 0.000 0.048
#&gt; ERR519493     5  0.5467    -0.1327 0.428 0.000 0.000 0.044 0.488 0.040
#&gt; ERR519514     1  0.1141     0.7254 0.948 0.000 0.000 0.000 0.052 0.000
#&gt; ERR519479     5  0.3555     0.4204 0.000 0.000 0.000 0.280 0.712 0.008
#&gt; ERR519509     1  0.1075     0.7119 0.952 0.000 0.000 0.000 0.000 0.048
#&gt; ERR519472     5  0.3668     0.3762 0.004 0.000 0.000 0.328 0.668 0.000
#&gt; ERR519510     6  0.6128     0.0871 0.000 0.000 0.000 0.340 0.316 0.344
#&gt; ERR519470     1  0.1141     0.7254 0.948 0.000 0.000 0.000 0.052 0.000
#&gt; ERR519495     5  0.4594     0.4239 0.092 0.000 0.000 0.232 0.676 0.000
#&gt; ERR519522     1  0.3332     0.6297 0.808 0.000 0.000 0.144 0.000 0.048
#&gt; ERR519523     4  0.2461     0.5193 0.064 0.000 0.000 0.888 0.044 0.004
#&gt; ERR519503     1  0.5324     0.3941 0.592 0.000 0.000 0.000 0.172 0.236
#&gt; ERR519471     1  0.1802     0.7173 0.916 0.000 0.000 0.000 0.072 0.012
#&gt; ERR519500     4  0.3852     0.3375 0.004 0.000 0.000 0.612 0.384 0.000
#&gt; ERR519485     1  0.4978     0.3630 0.532 0.000 0.000 0.000 0.396 0.072
#&gt; ERR519476     2  0.0806     0.9825 0.000 0.972 0.000 0.000 0.020 0.008
#&gt; ERR519502     4  0.4791     0.4653 0.000 0.000 0.000 0.652 0.244 0.104
#&gt; ERR519486     1  0.5040     0.3319 0.516 0.000 0.000 0.000 0.408 0.076
#&gt; ERR519478     1  0.1265     0.7155 0.948 0.000 0.000 0.000 0.008 0.044
#&gt; ERR519497     4  0.4136     0.3410 0.000 0.000 0.000 0.732 0.076 0.192
#&gt; ERR519467     1  0.4112     0.5866 0.724 0.000 0.000 0.224 0.004 0.048
#&gt; ERR519489     4  0.3986     0.3271 0.004 0.000 0.000 0.608 0.384 0.004
#&gt; ERR519494     3  0.3139     0.9021 0.000 0.000 0.816 0.000 0.032 0.152
#&gt; ERR519474     5  0.5751     0.2461 0.252 0.000 0.000 0.076 0.604 0.068
#&gt; ERR519505     6  0.4854     0.5152 0.000 0.000 0.000 0.264 0.100 0.636
#&gt; ERR519517     3  0.0458     0.9050 0.000 0.000 0.984 0.000 0.000 0.016
#&gt; ERR519484     5  0.5895    -0.2404 0.000 0.000 0.000 0.208 0.436 0.356
#&gt; ERR519498     6  0.4886     0.4056 0.000 0.000 0.000 0.432 0.060 0.508
#&gt; ERR519490     3  0.3139     0.9031 0.000 0.000 0.816 0.000 0.032 0.152
#&gt; ERR519507     5  0.3468     0.4296 0.000 0.000 0.000 0.264 0.728 0.008
#&gt; ERR519511     5  0.5753    -0.1657 0.000 0.000 0.000 0.384 0.444 0.172
#&gt; ERR519468     3  0.2815     0.9043 0.000 0.000 0.848 0.000 0.032 0.120
#&gt; ERR519482     3  0.3139     0.9031 0.000 0.000 0.816 0.000 0.032 0.152
#&gt; ERR519475     2  0.0000     0.9913 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; ERR519496     1  0.3934     0.5381 0.676 0.000 0.000 0.000 0.304 0.020
#&gt; ERR519506     5  0.5320     0.1580 0.144 0.000 0.000 0.000 0.576 0.280
#&gt; ERR519469     5  0.3684     0.3508 0.000 0.000 0.000 0.332 0.664 0.004
#&gt; ERR519480     3  0.1333     0.8975 0.000 0.000 0.944 0.000 0.008 0.048
#&gt; ERR519487     3  0.0363     0.9047 0.000 0.000 0.988 0.000 0.000 0.012
#&gt; ERR519483     5  0.5335     0.1493 0.148 0.000 0.000 0.000 0.576 0.276
#&gt; ERR519477     2  0.0000     0.9913 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; ERR519499     3  0.0363     0.9047 0.000 0.000 0.988 0.000 0.000 0.012
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-5-a').click(function(){
  $('#tab-SD-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-SD-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-get-signatures'>
<ul>
<li><a href='#tab-SD-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-kmeans-signature_compare](figure_cola/SD-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-SD-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-kmeans-collect-classes](figure_cola/SD-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:skmeans






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "skmeans"]
# you can also extract it by
# res = res_list["SD:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 18140 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-skmeans-collect-plots](figure_cola/SD-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-skmeans-select-partition-number](figure_cola/SD-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.687           0.876       0.942         0.4641 0.551   0.551
#> 3 3 0.889           0.889       0.947         0.4545 0.744   0.546
#> 4 4 0.871           0.809       0.911         0.0887 0.908   0.732
#> 5 5 0.749           0.703       0.852         0.0829 0.888   0.614
#> 6 6 0.798           0.669       0.824         0.0460 0.938   0.710
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-get-classes'>
<ul>
<li><a href='#tab-SD-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-skmeans-get-classes-1'>
<p><a id='tab-SD-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; ERR519515     1  0.0000      0.925 1.000 0.000
#&gt; ERR519516     1  0.0000      0.925 1.000 0.000
#&gt; ERR519520     1  0.0376      0.924 0.996 0.004
#&gt; ERR519513     2  0.0000      0.953 0.000 1.000
#&gt; ERR519481     1  0.7299      0.771 0.796 0.204
#&gt; ERR519491     1  0.0000      0.925 1.000 0.000
#&gt; ERR519473     1  0.7299      0.771 0.796 0.204
#&gt; ERR519518     1  0.9686      0.457 0.604 0.396
#&gt; ERR519512     1  0.0376      0.924 0.996 0.004
#&gt; ERR519521     1  0.0376      0.924 0.996 0.004
#&gt; ERR519488     1  0.0000      0.925 1.000 0.000
#&gt; ERR519493     1  0.0000      0.925 1.000 0.000
#&gt; ERR519514     1  0.0000      0.925 1.000 0.000
#&gt; ERR519479     1  0.0376      0.924 0.996 0.004
#&gt; ERR519509     1  0.0000      0.925 1.000 0.000
#&gt; ERR519472     1  0.0376      0.924 0.996 0.004
#&gt; ERR519510     1  0.6247      0.815 0.844 0.156
#&gt; ERR519470     1  0.0000      0.925 1.000 0.000
#&gt; ERR519495     1  0.0000      0.925 1.000 0.000
#&gt; ERR519522     1  0.0000      0.925 1.000 0.000
#&gt; ERR519523     1  0.0376      0.924 0.996 0.004
#&gt; ERR519503     2  0.7299      0.745 0.204 0.796
#&gt; ERR519471     1  0.0000      0.925 1.000 0.000
#&gt; ERR519500     1  0.0376      0.924 0.996 0.004
#&gt; ERR519485     1  0.0000      0.925 1.000 0.000
#&gt; ERR519476     2  0.0376      0.952 0.004 0.996
#&gt; ERR519502     1  0.7299      0.771 0.796 0.204
#&gt; ERR519486     1  0.0000      0.925 1.000 0.000
#&gt; ERR519478     1  0.0000      0.925 1.000 0.000
#&gt; ERR519497     1  0.9686      0.457 0.604 0.396
#&gt; ERR519467     1  0.0000      0.925 1.000 0.000
#&gt; ERR519489     1  0.0376      0.924 0.996 0.004
#&gt; ERR519494     2  0.0000      0.953 0.000 1.000
#&gt; ERR519474     1  0.0000      0.925 1.000 0.000
#&gt; ERR519505     2  0.0000      0.953 0.000 1.000
#&gt; ERR519517     2  0.0000      0.953 0.000 1.000
#&gt; ERR519484     1  0.9710      0.448 0.600 0.400
#&gt; ERR519498     2  0.7745      0.653 0.228 0.772
#&gt; ERR519490     2  0.0000      0.953 0.000 1.000
#&gt; ERR519507     1  0.6887      0.790 0.816 0.184
#&gt; ERR519511     1  0.7299      0.771 0.796 0.204
#&gt; ERR519468     2  0.0000      0.953 0.000 1.000
#&gt; ERR519482     2  0.0000      0.953 0.000 1.000
#&gt; ERR519475     2  0.0376      0.952 0.004 0.996
#&gt; ERR519496     1  0.0000      0.925 1.000 0.000
#&gt; ERR519506     2  0.0672      0.950 0.008 0.992
#&gt; ERR519469     1  0.0376      0.924 0.996 0.004
#&gt; ERR519480     2  0.0000      0.953 0.000 1.000
#&gt; ERR519487     2  0.0000      0.953 0.000 1.000
#&gt; ERR519483     2  0.7219      0.750 0.200 0.800
#&gt; ERR519477     2  0.0376      0.952 0.004 0.996
#&gt; ERR519499     2  0.0000      0.953 0.000 1.000
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-1-a').click(function(){
  $('#tab-SD-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-2'>
<p><a id='tab-SD-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; ERR519515     1  0.0000      0.933 1.000 0.000 0.000
#&gt; ERR519516     1  0.5327      0.632 0.728 0.272 0.000
#&gt; ERR519520     2  0.6154      0.325 0.408 0.592 0.000
#&gt; ERR519513     3  0.4931      0.716 0.000 0.232 0.768
#&gt; ERR519481     2  0.0424      0.940 0.008 0.992 0.000
#&gt; ERR519491     1  0.0747      0.933 0.984 0.016 0.000
#&gt; ERR519473     2  0.0000      0.938 0.000 1.000 0.000
#&gt; ERR519518     2  0.0747      0.929 0.000 0.984 0.016
#&gt; ERR519512     2  0.2711      0.876 0.088 0.912 0.000
#&gt; ERR519521     2  0.0592      0.940 0.012 0.988 0.000
#&gt; ERR519488     1  0.0592      0.926 0.988 0.000 0.012
#&gt; ERR519493     1  0.0747      0.933 0.984 0.016 0.000
#&gt; ERR519514     1  0.0237      0.934 0.996 0.004 0.000
#&gt; ERR519479     2  0.0747      0.939 0.016 0.984 0.000
#&gt; ERR519509     1  0.0592      0.926 0.988 0.000 0.012
#&gt; ERR519472     2  0.0892      0.937 0.020 0.980 0.000
#&gt; ERR519510     2  0.0592      0.940 0.012 0.988 0.000
#&gt; ERR519470     1  0.0000      0.933 1.000 0.000 0.000
#&gt; ERR519495     1  0.5905      0.420 0.648 0.352 0.000
#&gt; ERR519522     1  0.0747      0.933 0.984 0.016 0.000
#&gt; ERR519523     2  0.5785      0.508 0.332 0.668 0.000
#&gt; ERR519503     3  0.5138      0.664 0.252 0.000 0.748
#&gt; ERR519471     1  0.0000      0.933 1.000 0.000 0.000
#&gt; ERR519500     2  0.0892      0.937 0.020 0.980 0.000
#&gt; ERR519485     1  0.0424      0.929 0.992 0.000 0.008
#&gt; ERR519476     3  0.0747      0.950 0.016 0.000 0.984
#&gt; ERR519502     2  0.0000      0.938 0.000 1.000 0.000
#&gt; ERR519486     1  0.0747      0.933 0.984 0.016 0.000
#&gt; ERR519478     1  0.0237      0.934 0.996 0.004 0.000
#&gt; ERR519497     2  0.0747      0.929 0.000 0.984 0.016
#&gt; ERR519467     1  0.0747      0.933 0.984 0.016 0.000
#&gt; ERR519489     2  0.1031      0.934 0.024 0.976 0.000
#&gt; ERR519494     3  0.0892      0.955 0.000 0.020 0.980
#&gt; ERR519474     1  0.4750      0.722 0.784 0.216 0.000
#&gt; ERR519505     3  0.0892      0.952 0.000 0.020 0.980
#&gt; ERR519517     3  0.0892      0.955 0.000 0.020 0.980
#&gt; ERR519484     2  0.0000      0.938 0.000 1.000 0.000
#&gt; ERR519498     2  0.0747      0.929 0.000 0.984 0.016
#&gt; ERR519490     3  0.0892      0.955 0.000 0.020 0.980
#&gt; ERR519507     2  0.0592      0.940 0.012 0.988 0.000
#&gt; ERR519511     2  0.0592      0.940 0.012 0.988 0.000
#&gt; ERR519468     3  0.0892      0.955 0.000 0.020 0.980
#&gt; ERR519482     3  0.0892      0.955 0.000 0.020 0.980
#&gt; ERR519475     3  0.0747      0.950 0.016 0.000 0.984
#&gt; ERR519496     1  0.0747      0.933 0.984 0.016 0.000
#&gt; ERR519506     3  0.0747      0.950 0.016 0.000 0.984
#&gt; ERR519469     2  0.0424      0.934 0.000 0.992 0.008
#&gt; ERR519480     3  0.0592      0.955 0.000 0.012 0.988
#&gt; ERR519487     3  0.0747      0.956 0.000 0.016 0.984
#&gt; ERR519483     3  0.0892      0.948 0.020 0.000 0.980
#&gt; ERR519477     3  0.0747      0.950 0.016 0.000 0.984
#&gt; ERR519499     3  0.0747      0.956 0.000 0.016 0.984
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-2-a').click(function(){
  $('#tab-SD-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-3'>
<p><a id='tab-SD-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; ERR519515     1  0.0000      0.926 1.000 0.000 0.000 0.000
#&gt; ERR519516     1  0.4855      0.462 0.644 0.004 0.000 0.352
#&gt; ERR519520     4  0.5336      0.118 0.492 0.004 0.004 0.500
#&gt; ERR519513     3  0.0804      0.914 0.000 0.008 0.980 0.012
#&gt; ERR519481     4  0.0188      0.838 0.000 0.000 0.004 0.996
#&gt; ERR519491     1  0.0000      0.926 1.000 0.000 0.000 0.000
#&gt; ERR519473     4  0.1909      0.834 0.008 0.048 0.004 0.940
#&gt; ERR519518     4  0.4800      0.485 0.000 0.004 0.340 0.656
#&gt; ERR519512     4  0.3072      0.775 0.124 0.004 0.004 0.868
#&gt; ERR519521     4  0.0564      0.837 0.004 0.004 0.004 0.988
#&gt; ERR519488     1  0.0376      0.924 0.992 0.004 0.000 0.004
#&gt; ERR519493     1  0.1209      0.906 0.964 0.032 0.000 0.004
#&gt; ERR519514     1  0.0000      0.926 1.000 0.000 0.000 0.000
#&gt; ERR519479     4  0.1722      0.834 0.008 0.048 0.000 0.944
#&gt; ERR519509     1  0.0376      0.924 0.992 0.004 0.000 0.004
#&gt; ERR519472     4  0.1722      0.834 0.008 0.048 0.000 0.944
#&gt; ERR519510     4  0.1042      0.834 0.000 0.008 0.020 0.972
#&gt; ERR519470     1  0.0000      0.926 1.000 0.000 0.000 0.000
#&gt; ERR519495     4  0.6149      0.157 0.472 0.048 0.000 0.480
#&gt; ERR519522     1  0.0376      0.924 0.992 0.004 0.000 0.004
#&gt; ERR519523     4  0.4897      0.539 0.324 0.004 0.004 0.668
#&gt; ERR519503     2  0.1661      0.929 0.052 0.944 0.004 0.000
#&gt; ERR519471     1  0.0000      0.926 1.000 0.000 0.000 0.000
#&gt; ERR519500     4  0.0672      0.838 0.008 0.008 0.000 0.984
#&gt; ERR519485     1  0.1004      0.911 0.972 0.024 0.000 0.004
#&gt; ERR519476     2  0.1637      0.959 0.000 0.940 0.060 0.000
#&gt; ERR519502     4  0.0469      0.837 0.000 0.000 0.012 0.988
#&gt; ERR519486     1  0.1109      0.909 0.968 0.028 0.000 0.004
#&gt; ERR519478     1  0.0376      0.924 0.992 0.004 0.000 0.004
#&gt; ERR519497     4  0.4905      0.442 0.000 0.004 0.364 0.632
#&gt; ERR519467     1  0.0376      0.924 0.992 0.004 0.000 0.004
#&gt; ERR519489     4  0.0672      0.838 0.008 0.008 0.000 0.984
#&gt; ERR519494     3  0.0592      0.939 0.000 0.016 0.984 0.000
#&gt; ERR519474     1  0.6120      0.145 0.520 0.048 0.000 0.432
#&gt; ERR519505     3  0.5950      0.196 0.000 0.416 0.544 0.040
#&gt; ERR519517     3  0.0592      0.939 0.000 0.016 0.984 0.000
#&gt; ERR519484     4  0.2089      0.833 0.000 0.048 0.020 0.932
#&gt; ERR519498     3  0.1970      0.869 0.000 0.008 0.932 0.060
#&gt; ERR519490     3  0.0592      0.939 0.000 0.016 0.984 0.000
#&gt; ERR519507     4  0.1909      0.834 0.008 0.048 0.004 0.940
#&gt; ERR519511     4  0.1059      0.835 0.000 0.012 0.016 0.972
#&gt; ERR519468     3  0.0592      0.939 0.000 0.016 0.984 0.000
#&gt; ERR519482     3  0.0592      0.939 0.000 0.016 0.984 0.000
#&gt; ERR519475     2  0.1637      0.959 0.000 0.940 0.060 0.000
#&gt; ERR519496     1  0.0000      0.926 1.000 0.000 0.000 0.000
#&gt; ERR519506     2  0.0657      0.949 0.004 0.984 0.012 0.000
#&gt; ERR519469     4  0.1909      0.834 0.008 0.048 0.004 0.940
#&gt; ERR519480     3  0.0592      0.939 0.000 0.016 0.984 0.000
#&gt; ERR519487     3  0.0592      0.939 0.000 0.016 0.984 0.000
#&gt; ERR519483     2  0.0657      0.949 0.004 0.984 0.012 0.000
#&gt; ERR519477     2  0.1637      0.959 0.000 0.940 0.060 0.000
#&gt; ERR519499     3  0.0592      0.939 0.000 0.016 0.984 0.000
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-3-a').click(function(){
  $('#tab-SD-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-4'>
<p><a id='tab-SD-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; ERR519515     1  0.0000     0.9204 1.000 0.000 0.000 0.000 0.000
#&gt; ERR519516     1  0.5708     0.3100 0.528 0.000 0.000 0.384 0.088
#&gt; ERR519520     4  0.1965     0.6191 0.096 0.000 0.000 0.904 0.000
#&gt; ERR519513     3  0.3812     0.7250 0.000 0.000 0.772 0.024 0.204
#&gt; ERR519481     5  0.4304     0.2933 0.000 0.000 0.000 0.484 0.516
#&gt; ERR519491     1  0.1956     0.8933 0.928 0.008 0.000 0.012 0.052
#&gt; ERR519473     5  0.4467     0.5529 0.000 0.016 0.000 0.344 0.640
#&gt; ERR519518     4  0.4365     0.5676 0.000 0.000 0.116 0.768 0.116
#&gt; ERR519512     4  0.0609     0.6456 0.020 0.000 0.000 0.980 0.000
#&gt; ERR519521     4  0.0290     0.6432 0.000 0.000 0.000 0.992 0.008
#&gt; ERR519488     1  0.0162     0.9202 0.996 0.000 0.000 0.004 0.000
#&gt; ERR519493     1  0.4061     0.7554 0.776 0.012 0.000 0.024 0.188
#&gt; ERR519514     1  0.0000     0.9204 1.000 0.000 0.000 0.000 0.000
#&gt; ERR519479     5  0.3807     0.6101 0.000 0.012 0.000 0.240 0.748
#&gt; ERR519509     1  0.0162     0.9202 0.996 0.000 0.000 0.004 0.000
#&gt; ERR519472     5  0.4610     0.5279 0.000 0.016 0.000 0.388 0.596
#&gt; ERR519510     5  0.3274     0.3361 0.000 0.000 0.000 0.220 0.780
#&gt; ERR519470     1  0.0000     0.9204 1.000 0.000 0.000 0.000 0.000
#&gt; ERR519495     5  0.6342     0.4816 0.192 0.012 0.000 0.220 0.576
#&gt; ERR519522     1  0.0162     0.9202 0.996 0.000 0.000 0.004 0.000
#&gt; ERR519523     4  0.2624     0.5716 0.116 0.000 0.000 0.872 0.012
#&gt; ERR519503     2  0.1270     0.8512 0.052 0.948 0.000 0.000 0.000
#&gt; ERR519471     1  0.0000     0.9204 1.000 0.000 0.000 0.000 0.000
#&gt; ERR519500     4  0.3305     0.3613 0.000 0.000 0.000 0.776 0.224
#&gt; ERR519485     1  0.2074     0.8902 0.920 0.016 0.000 0.004 0.060
#&gt; ERR519476     2  0.0609     0.8814 0.000 0.980 0.020 0.000 0.000
#&gt; ERR519502     4  0.4171     0.0633 0.000 0.000 0.000 0.604 0.396
#&gt; ERR519486     1  0.3005     0.8456 0.856 0.012 0.000 0.008 0.124
#&gt; ERR519478     1  0.0162     0.9202 0.996 0.000 0.000 0.004 0.000
#&gt; ERR519497     4  0.5373     0.4831 0.000 0.000 0.112 0.652 0.236
#&gt; ERR519467     1  0.2179     0.8453 0.888 0.000 0.000 0.112 0.000
#&gt; ERR519489     4  0.1908     0.5861 0.000 0.000 0.000 0.908 0.092
#&gt; ERR519494     3  0.0290     0.9636 0.000 0.000 0.992 0.000 0.008
#&gt; ERR519474     5  0.6899     0.1859 0.352 0.012 0.000 0.208 0.428
#&gt; ERR519505     2  0.8376     0.1064 0.000 0.352 0.196 0.176 0.276
#&gt; ERR519517     3  0.0000     0.9640 0.000 0.000 1.000 0.000 0.000
#&gt; ERR519484     5  0.1365     0.5088 0.000 0.004 0.004 0.040 0.952
#&gt; ERR519498     4  0.6556     0.3195 0.000 0.000 0.264 0.476 0.260
#&gt; ERR519490     3  0.0404     0.9628 0.000 0.000 0.988 0.000 0.012
#&gt; ERR519507     5  0.3819     0.6116 0.000 0.016 0.000 0.228 0.756
#&gt; ERR519511     5  0.2329     0.4580 0.000 0.000 0.000 0.124 0.876
#&gt; ERR519468     3  0.0404     0.9628 0.000 0.000 0.988 0.000 0.012
#&gt; ERR519482     3  0.0404     0.9628 0.000 0.000 0.988 0.000 0.012
#&gt; ERR519475     2  0.0609     0.8814 0.000 0.980 0.020 0.000 0.000
#&gt; ERR519496     1  0.0510     0.9158 0.984 0.000 0.000 0.000 0.016
#&gt; ERR519506     2  0.0000     0.8764 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519469     5  0.4737     0.5245 0.000 0.016 0.004 0.380 0.600
#&gt; ERR519480     3  0.0000     0.9640 0.000 0.000 1.000 0.000 0.000
#&gt; ERR519487     3  0.0000     0.9640 0.000 0.000 1.000 0.000 0.000
#&gt; ERR519483     2  0.0404     0.8712 0.000 0.988 0.000 0.000 0.012
#&gt; ERR519477     2  0.0609     0.8814 0.000 0.980 0.020 0.000 0.000
#&gt; ERR519499     3  0.0000     0.9640 0.000 0.000 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-4-a').click(function(){
  $('#tab-SD-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-5'>
<p><a id='tab-SD-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; ERR519515     1  0.0146    0.85025 0.996 0.000 0.000 0.000 0.000 0.004
#&gt; ERR519516     4  0.6582   -0.16176 0.380 0.000 0.000 0.428 0.084 0.108
#&gt; ERR519520     4  0.1367    0.61125 0.044 0.000 0.000 0.944 0.000 0.012
#&gt; ERR519513     6  0.3986    0.14953 0.000 0.000 0.464 0.004 0.000 0.532
#&gt; ERR519481     5  0.5959    0.00524 0.000 0.000 0.000 0.260 0.452 0.288
#&gt; ERR519491     1  0.4715    0.73903 0.736 0.000 0.000 0.048 0.080 0.136
#&gt; ERR519473     5  0.1858    0.70645 0.000 0.000 0.000 0.092 0.904 0.004
#&gt; ERR519518     4  0.5791    0.20104 0.000 0.000 0.076 0.560 0.052 0.312
#&gt; ERR519512     4  0.0964    0.62516 0.016 0.000 0.000 0.968 0.012 0.004
#&gt; ERR519521     4  0.1700    0.62120 0.000 0.000 0.000 0.928 0.048 0.024
#&gt; ERR519488     1  0.1633    0.83997 0.932 0.000 0.000 0.044 0.000 0.024
#&gt; ERR519493     1  0.6347    0.52433 0.548 0.000 0.000 0.060 0.200 0.192
#&gt; ERR519514     1  0.0146    0.85025 0.996 0.000 0.000 0.000 0.000 0.004
#&gt; ERR519479     5  0.2039    0.67606 0.000 0.000 0.000 0.020 0.904 0.076
#&gt; ERR519509     1  0.1633    0.83997 0.932 0.000 0.000 0.044 0.000 0.024
#&gt; ERR519472     5  0.1812    0.71340 0.000 0.000 0.000 0.080 0.912 0.008
#&gt; ERR519510     6  0.3736    0.61851 0.000 0.000 0.000 0.068 0.156 0.776
#&gt; ERR519470     1  0.0146    0.85025 0.996 0.000 0.000 0.000 0.000 0.004
#&gt; ERR519495     5  0.2831    0.67540 0.056 0.000 0.000 0.036 0.876 0.032
#&gt; ERR519522     1  0.1745    0.83750 0.924 0.000 0.000 0.056 0.000 0.020
#&gt; ERR519523     4  0.1863    0.61777 0.060 0.000 0.000 0.920 0.016 0.004
#&gt; ERR519503     2  0.3084    0.80014 0.136 0.832 0.000 0.008 0.000 0.024
#&gt; ERR519471     1  0.0547    0.84869 0.980 0.000 0.000 0.000 0.000 0.020
#&gt; ERR519500     4  0.4066    0.42171 0.004 0.000 0.000 0.696 0.272 0.028
#&gt; ERR519485     1  0.4430    0.72905 0.732 0.004 0.000 0.012 0.064 0.188
#&gt; ERR519476     2  0.0000    0.94376 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; ERR519502     4  0.6102    0.01383 0.000 0.000 0.000 0.376 0.292 0.332
#&gt; ERR519486     1  0.5243    0.62273 0.616 0.000 0.000 0.016 0.092 0.276
#&gt; ERR519478     1  0.1549    0.84068 0.936 0.000 0.000 0.044 0.000 0.020
#&gt; ERR519497     4  0.4829    0.00660 0.000 0.000 0.056 0.520 0.000 0.424
#&gt; ERR519467     1  0.3974    0.57366 0.680 0.000 0.000 0.296 0.000 0.024
#&gt; ERR519489     4  0.3062    0.57327 0.000 0.000 0.000 0.824 0.144 0.032
#&gt; ERR519494     3  0.0146    0.99443 0.000 0.000 0.996 0.000 0.000 0.004
#&gt; ERR519474     5  0.7659   -0.02209 0.276 0.000 0.000 0.200 0.304 0.220
#&gt; ERR519505     6  0.4909    0.57314 0.000 0.104 0.068 0.100 0.000 0.728
#&gt; ERR519517     3  0.0000    0.99921 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519484     6  0.3725    0.51068 0.000 0.000 0.000 0.008 0.316 0.676
#&gt; ERR519498     6  0.4570    0.49317 0.000 0.000 0.092 0.228 0.000 0.680
#&gt; ERR519490     3  0.0000    0.99921 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519507     5  0.1616    0.68905 0.000 0.000 0.000 0.020 0.932 0.048
#&gt; ERR519511     6  0.4498    0.50576 0.000 0.000 0.000 0.056 0.300 0.644
#&gt; ERR519468     3  0.0000    0.99921 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519482     3  0.0000    0.99921 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519475     2  0.0000    0.94376 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; ERR519496     1  0.1644    0.83421 0.932 0.000 0.000 0.004 0.012 0.052
#&gt; ERR519506     2  0.0291    0.94200 0.000 0.992 0.000 0.004 0.000 0.004
#&gt; ERR519469     5  0.2191    0.69357 0.000 0.000 0.004 0.120 0.876 0.000
#&gt; ERR519480     3  0.0000    0.99921 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519487     3  0.0000    0.99921 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519483     2  0.1994    0.90133 0.016 0.920 0.000 0.008 0.004 0.052
#&gt; ERR519477     2  0.0000    0.94376 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; ERR519499     3  0.0000    0.99921 0.000 0.000 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-5-a').click(function(){
  $('#tab-SD-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-SD-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-get-signatures'>
<ul>
<li><a href='#tab-SD-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-skmeans-signature_compare](figure_cola/SD-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-SD-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-skmeans-collect-classes](figure_cola/SD-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:pam*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "pam"]
# you can also extract it by
# res = res_list["SD:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 18140 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 4.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-pam-collect-plots](figure_cola/SD-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-pam-select-partition-number](figure_cola/SD-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000          0.112 0.889   0.889
#> 3 3 0.635           0.909       0.950          2.727 0.729   0.695
#> 4 4 0.906           0.890       0.954          0.539 0.705   0.537
#> 5 5 0.787           0.813       0.911          0.149 0.894   0.715
#> 6 6 0.807           0.767       0.881          0.102 0.852   0.516
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 4
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-pam-get-classes'>
<ul>
<li><a href='#tab-SD-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-pam-get-classes-1'>
<p><a id='tab-SD-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette p1 p2
#&gt; ERR519515     1       0          1  1  0
#&gt; ERR519516     1       0          1  1  0
#&gt; ERR519520     1       0          1  1  0
#&gt; ERR519513     1       0          1  1  0
#&gt; ERR519481     1       0          1  1  0
#&gt; ERR519491     1       0          1  1  0
#&gt; ERR519473     1       0          1  1  0
#&gt; ERR519518     1       0          1  1  0
#&gt; ERR519512     1       0          1  1  0
#&gt; ERR519521     1       0          1  1  0
#&gt; ERR519488     1       0          1  1  0
#&gt; ERR519493     1       0          1  1  0
#&gt; ERR519514     1       0          1  1  0
#&gt; ERR519479     1       0          1  1  0
#&gt; ERR519509     1       0          1  1  0
#&gt; ERR519472     1       0          1  1  0
#&gt; ERR519510     1       0          1  1  0
#&gt; ERR519470     1       0          1  1  0
#&gt; ERR519495     1       0          1  1  0
#&gt; ERR519522     1       0          1  1  0
#&gt; ERR519523     1       0          1  1  0
#&gt; ERR519503     1       0          1  1  0
#&gt; ERR519471     1       0          1  1  0
#&gt; ERR519500     1       0          1  1  0
#&gt; ERR519485     1       0          1  1  0
#&gt; ERR519476     2       0          1  0  1
#&gt; ERR519502     1       0          1  1  0
#&gt; ERR519486     1       0          1  1  0
#&gt; ERR519478     1       0          1  1  0
#&gt; ERR519497     1       0          1  1  0
#&gt; ERR519467     1       0          1  1  0
#&gt; ERR519489     1       0          1  1  0
#&gt; ERR519494     1       0          1  1  0
#&gt; ERR519474     1       0          1  1  0
#&gt; ERR519505     1       0          1  1  0
#&gt; ERR519517     1       0          1  1  0
#&gt; ERR519484     1       0          1  1  0
#&gt; ERR519498     1       0          1  1  0
#&gt; ERR519490     1       0          1  1  0
#&gt; ERR519507     1       0          1  1  0
#&gt; ERR519511     1       0          1  1  0
#&gt; ERR519468     1       0          1  1  0
#&gt; ERR519482     1       0          1  1  0
#&gt; ERR519475     2       0          1  0  1
#&gt; ERR519496     1       0          1  1  0
#&gt; ERR519506     1       0          1  1  0
#&gt; ERR519469     1       0          1  1  0
#&gt; ERR519480     1       0          1  1  0
#&gt; ERR519487     1       0          1  1  0
#&gt; ERR519483     1       0          1  1  0
#&gt; ERR519477     2       0          1  0  1
#&gt; ERR519499     1       0          1  1  0
</code></pre>

<script>
$('#tab-SD-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-1-a').click(function(){
  $('#tab-SD-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-2'>
<p><a id='tab-SD-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3
#&gt; ERR519515     1  0.0000      0.932 1.000  0 0.000
#&gt; ERR519516     1  0.0237      0.931 0.996  0 0.004
#&gt; ERR519520     1  0.0000      0.932 1.000  0 0.000
#&gt; ERR519513     3  0.0000      0.965 0.000  0 1.000
#&gt; ERR519481     1  0.3686      0.883 0.860  0 0.140
#&gt; ERR519491     1  0.0000      0.932 1.000  0 0.000
#&gt; ERR519473     1  0.3686      0.883 0.860  0 0.140
#&gt; ERR519518     1  0.6308      0.210 0.508  0 0.492
#&gt; ERR519512     1  0.0237      0.931 0.996  0 0.004
#&gt; ERR519521     1  0.3686      0.883 0.860  0 0.140
#&gt; ERR519488     1  0.0000      0.932 1.000  0 0.000
#&gt; ERR519493     1  0.0000      0.932 1.000  0 0.000
#&gt; ERR519514     1  0.0000      0.932 1.000  0 0.000
#&gt; ERR519479     1  0.3686      0.883 0.860  0 0.140
#&gt; ERR519509     1  0.0000      0.932 1.000  0 0.000
#&gt; ERR519472     1  0.0000      0.932 1.000  0 0.000
#&gt; ERR519510     1  0.3686      0.883 0.860  0 0.140
#&gt; ERR519470     1  0.0000      0.932 1.000  0 0.000
#&gt; ERR519495     1  0.0000      0.932 1.000  0 0.000
#&gt; ERR519522     1  0.0000      0.932 1.000  0 0.000
#&gt; ERR519523     1  0.0000      0.932 1.000  0 0.000
#&gt; ERR519503     1  0.0000      0.932 1.000  0 0.000
#&gt; ERR519471     1  0.0000      0.932 1.000  0 0.000
#&gt; ERR519500     1  0.0237      0.931 0.996  0 0.004
#&gt; ERR519485     1  0.0000      0.932 1.000  0 0.000
#&gt; ERR519476     2  0.0000      1.000 0.000  1 0.000
#&gt; ERR519502     1  0.3686      0.883 0.860  0 0.140
#&gt; ERR519486     1  0.0000      0.932 1.000  0 0.000
#&gt; ERR519478     1  0.0000      0.932 1.000  0 0.000
#&gt; ERR519497     1  0.3686      0.883 0.860  0 0.140
#&gt; ERR519467     1  0.0000      0.932 1.000  0 0.000
#&gt; ERR519489     1  0.3686      0.883 0.860  0 0.140
#&gt; ERR519494     3  0.0000      0.965 0.000  0 1.000
#&gt; ERR519474     1  0.0000      0.932 1.000  0 0.000
#&gt; ERR519505     1  0.3686      0.883 0.860  0 0.140
#&gt; ERR519517     3  0.0000      0.965 0.000  0 1.000
#&gt; ERR519484     1  0.3686      0.883 0.860  0 0.140
#&gt; ERR519498     1  0.4062      0.862 0.836  0 0.164
#&gt; ERR519490     3  0.0000      0.965 0.000  0 1.000
#&gt; ERR519507     1  0.3619      0.885 0.864  0 0.136
#&gt; ERR519511     1  0.3686      0.883 0.860  0 0.140
#&gt; ERR519468     3  0.3686      0.702 0.140  0 0.860
#&gt; ERR519482     3  0.0000      0.965 0.000  0 1.000
#&gt; ERR519475     2  0.0000      1.000 0.000  1 0.000
#&gt; ERR519496     1  0.0000      0.932 1.000  0 0.000
#&gt; ERR519506     1  0.3267      0.893 0.884  0 0.116
#&gt; ERR519469     1  0.0000      0.932 1.000  0 0.000
#&gt; ERR519480     3  0.0000      0.965 0.000  0 1.000
#&gt; ERR519487     3  0.0000      0.965 0.000  0 1.000
#&gt; ERR519483     1  0.0000      0.932 1.000  0 0.000
#&gt; ERR519477     2  0.0000      1.000 0.000  1 0.000
#&gt; ERR519499     3  0.0000      0.965 0.000  0 1.000
</code></pre>

<script>
$('#tab-SD-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-2-a').click(function(){
  $('#tab-SD-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-3'>
<p><a id='tab-SD-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3    p4
#&gt; ERR519515     1  0.0000      0.946 1.000  0 0.000 0.000
#&gt; ERR519516     1  0.1940      0.918 0.924  0 0.000 0.076
#&gt; ERR519520     1  0.1118      0.933 0.964  0 0.000 0.036
#&gt; ERR519513     4  0.1940      0.824 0.000  0 0.076 0.924
#&gt; ERR519481     4  0.0000      0.890 0.000  0 0.000 1.000
#&gt; ERR519491     1  0.0000      0.946 1.000  0 0.000 0.000
#&gt; ERR519473     1  0.2216      0.907 0.908  0 0.000 0.092
#&gt; ERR519518     4  0.0000      0.890 0.000  0 0.000 1.000
#&gt; ERR519512     1  0.3726      0.770 0.788  0 0.000 0.212
#&gt; ERR519521     4  0.0000      0.890 0.000  0 0.000 1.000
#&gt; ERR519488     1  0.0000      0.946 1.000  0 0.000 0.000
#&gt; ERR519493     1  0.3266      0.829 0.832  0 0.000 0.168
#&gt; ERR519514     1  0.0000      0.946 1.000  0 0.000 0.000
#&gt; ERR519479     4  0.0188      0.888 0.004  0 0.000 0.996
#&gt; ERR519509     1  0.0000      0.946 1.000  0 0.000 0.000
#&gt; ERR519472     1  0.1792      0.923 0.932  0 0.000 0.068
#&gt; ERR519510     4  0.0188      0.888 0.004  0 0.000 0.996
#&gt; ERR519470     1  0.0000      0.946 1.000  0 0.000 0.000
#&gt; ERR519495     1  0.0000      0.946 1.000  0 0.000 0.000
#&gt; ERR519522     1  0.0000      0.946 1.000  0 0.000 0.000
#&gt; ERR519523     1  0.1389      0.933 0.952  0 0.000 0.048
#&gt; ERR519503     1  0.0000      0.946 1.000  0 0.000 0.000
#&gt; ERR519471     1  0.0000      0.946 1.000  0 0.000 0.000
#&gt; ERR519500     1  0.1557      0.931 0.944  0 0.000 0.056
#&gt; ERR519485     1  0.0000      0.946 1.000  0 0.000 0.000
#&gt; ERR519476     2  0.0000      1.000 0.000  1 0.000 0.000
#&gt; ERR519502     4  0.0000      0.890 0.000  0 0.000 1.000
#&gt; ERR519486     1  0.1118      0.938 0.964  0 0.000 0.036
#&gt; ERR519478     1  0.0000      0.946 1.000  0 0.000 0.000
#&gt; ERR519497     4  0.0000      0.890 0.000  0 0.000 1.000
#&gt; ERR519467     1  0.0000      0.946 1.000  0 0.000 0.000
#&gt; ERR519489     1  0.4746      0.475 0.632  0 0.000 0.368
#&gt; ERR519494     4  0.4605      0.471 0.000  0 0.336 0.664
#&gt; ERR519474     4  0.4999     -0.103 0.492  0 0.000 0.508
#&gt; ERR519505     4  0.0000      0.890 0.000  0 0.000 1.000
#&gt; ERR519517     3  0.0000      1.000 0.000  0 1.000 0.000
#&gt; ERR519484     4  0.0000      0.890 0.000  0 0.000 1.000
#&gt; ERR519498     4  0.1109      0.866 0.004  0 0.028 0.968
#&gt; ERR519490     3  0.0000      1.000 0.000  0 1.000 0.000
#&gt; ERR519507     4  0.3123      0.704 0.156  0 0.000 0.844
#&gt; ERR519511     4  0.0000      0.890 0.000  0 0.000 1.000
#&gt; ERR519468     3  0.0000      1.000 0.000  0 1.000 0.000
#&gt; ERR519482     3  0.0000      1.000 0.000  0 1.000 0.000
#&gt; ERR519475     2  0.0000      1.000 0.000  1 0.000 0.000
#&gt; ERR519496     1  0.0000      0.946 1.000  0 0.000 0.000
#&gt; ERR519506     1  0.1716      0.926 0.936  0 0.000 0.064
#&gt; ERR519469     1  0.1389      0.933 0.952  0 0.000 0.048
#&gt; ERR519480     3  0.0000      1.000 0.000  0 1.000 0.000
#&gt; ERR519487     3  0.0000      1.000 0.000  0 1.000 0.000
#&gt; ERR519483     1  0.0336      0.945 0.992  0 0.000 0.008
#&gt; ERR519477     2  0.0000      1.000 0.000  1 0.000 0.000
#&gt; ERR519499     3  0.0000      1.000 0.000  0 1.000 0.000
</code></pre>

<script>
$('#tab-SD-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-3-a').click(function(){
  $('#tab-SD-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-4'>
<p><a id='tab-SD-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3    p4    p5
#&gt; ERR519515     1  0.0000      0.868 1.000  0 0.000 0.000 0.000
#&gt; ERR519516     1  0.4793      0.702 0.700  0 0.000 0.068 0.232
#&gt; ERR519520     4  0.0290      0.944 0.008  0 0.000 0.992 0.000
#&gt; ERR519513     5  0.3707      0.510 0.000  0 0.284 0.000 0.716
#&gt; ERR519481     5  0.0000      0.816 0.000  0 0.000 0.000 1.000
#&gt; ERR519491     1  0.0609      0.865 0.980  0 0.000 0.020 0.000
#&gt; ERR519473     1  0.3999      0.617 0.656  0 0.000 0.000 0.344
#&gt; ERR519518     4  0.1043      0.924 0.000  0 0.000 0.960 0.040
#&gt; ERR519512     4  0.0290      0.944 0.008  0 0.000 0.992 0.000
#&gt; ERR519521     4  0.0671      0.937 0.004  0 0.000 0.980 0.016
#&gt; ERR519488     1  0.0290      0.866 0.992  0 0.000 0.008 0.000
#&gt; ERR519493     1  0.4437      0.637 0.664  0 0.000 0.020 0.316
#&gt; ERR519514     1  0.0000      0.868 1.000  0 0.000 0.000 0.000
#&gt; ERR519479     5  0.0898      0.803 0.008  0 0.000 0.020 0.972
#&gt; ERR519509     1  0.0290      0.866 0.992  0 0.000 0.008 0.000
#&gt; ERR519472     1  0.4526      0.653 0.672  0 0.000 0.028 0.300
#&gt; ERR519510     5  0.0324      0.813 0.004  0 0.000 0.004 0.992
#&gt; ERR519470     1  0.0000      0.868 1.000  0 0.000 0.000 0.000
#&gt; ERR519495     1  0.0000      0.868 1.000  0 0.000 0.000 0.000
#&gt; ERR519522     1  0.0290      0.866 0.992  0 0.000 0.008 0.000
#&gt; ERR519523     4  0.0671      0.937 0.016  0 0.000 0.980 0.004
#&gt; ERR519503     1  0.0290      0.866 0.992  0 0.000 0.008 0.000
#&gt; ERR519471     1  0.0000      0.868 1.000  0 0.000 0.000 0.000
#&gt; ERR519500     1  0.4524      0.556 0.644  0 0.000 0.336 0.020
#&gt; ERR519485     1  0.0609      0.865 0.980  0 0.000 0.020 0.000
#&gt; ERR519476     2  0.0000      1.000 0.000  1 0.000 0.000 0.000
#&gt; ERR519502     5  0.0000      0.816 0.000  0 0.000 0.000 1.000
#&gt; ERR519486     1  0.3151      0.799 0.836  0 0.000 0.020 0.144
#&gt; ERR519478     1  0.0290      0.866 0.992  0 0.000 0.008 0.000
#&gt; ERR519497     4  0.3003      0.758 0.000  0 0.000 0.812 0.188
#&gt; ERR519467     1  0.2471      0.807 0.864  0 0.000 0.136 0.000
#&gt; ERR519489     4  0.0290      0.944 0.008  0 0.000 0.992 0.000
#&gt; ERR519494     5  0.4060      0.414 0.000  0 0.360 0.000 0.640
#&gt; ERR519474     5  0.4829     -0.264 0.480  0 0.000 0.020 0.500
#&gt; ERR519505     5  0.0000      0.816 0.000  0 0.000 0.000 1.000
#&gt; ERR519517     3  0.0000      1.000 0.000  0 1.000 0.000 0.000
#&gt; ERR519484     5  0.0000      0.816 0.000  0 0.000 0.000 1.000
#&gt; ERR519498     5  0.3636      0.482 0.000  0 0.000 0.272 0.728
#&gt; ERR519490     3  0.0000      1.000 0.000  0 1.000 0.000 0.000
#&gt; ERR519507     5  0.1106      0.797 0.024  0 0.000 0.012 0.964
#&gt; ERR519511     5  0.0000      0.816 0.000  0 0.000 0.000 1.000
#&gt; ERR519468     3  0.0000      1.000 0.000  0 1.000 0.000 0.000
#&gt; ERR519482     3  0.0000      1.000 0.000  0 1.000 0.000 0.000
#&gt; ERR519475     2  0.0000      1.000 0.000  1 0.000 0.000 0.000
#&gt; ERR519496     1  0.0000      0.868 1.000  0 0.000 0.000 0.000
#&gt; ERR519506     1  0.4213      0.656 0.680  0 0.000 0.012 0.308
#&gt; ERR519469     1  0.4404      0.688 0.704  0 0.000 0.032 0.264
#&gt; ERR519480     3  0.0000      1.000 0.000  0 1.000 0.000 0.000
#&gt; ERR519487     3  0.0000      1.000 0.000  0 1.000 0.000 0.000
#&gt; ERR519483     1  0.1012      0.863 0.968  0 0.000 0.020 0.012
#&gt; ERR519477     2  0.0000      1.000 0.000  1 0.000 0.000 0.000
#&gt; ERR519499     3  0.0000      1.000 0.000  0 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-4-a').click(function(){
  $('#tab-SD-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-5'>
<p><a id='tab-SD-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3    p4    p5    p6
#&gt; ERR519515     1  0.0000      0.899 1.000  0 0.000 0.000 0.000 0.000
#&gt; ERR519516     1  0.5873      0.109 0.508  0 0.000 0.028 0.108 0.356
#&gt; ERR519520     4  0.0000      0.866 0.000  0 0.000 1.000 0.000 0.000
#&gt; ERR519513     5  0.2178      0.688 0.000  0 0.132 0.000 0.868 0.000
#&gt; ERR519481     5  0.3804      0.232 0.000  0 0.000 0.000 0.576 0.424
#&gt; ERR519491     1  0.0260      0.897 0.992  0 0.000 0.000 0.000 0.008
#&gt; ERR519473     6  0.1663      0.757 0.000  0 0.000 0.000 0.088 0.912
#&gt; ERR519518     4  0.1765      0.821 0.000  0 0.000 0.904 0.096 0.000
#&gt; ERR519512     4  0.0000      0.866 0.000  0 0.000 1.000 0.000 0.000
#&gt; ERR519521     4  0.0000      0.866 0.000  0 0.000 1.000 0.000 0.000
#&gt; ERR519488     1  0.1556      0.883 0.920  0 0.000 0.000 0.000 0.080
#&gt; ERR519493     5  0.5008      0.442 0.280  0 0.000 0.000 0.612 0.108
#&gt; ERR519514     1  0.0000      0.899 1.000  0 0.000 0.000 0.000 0.000
#&gt; ERR519479     6  0.4072      0.260 0.008  0 0.000 0.000 0.448 0.544
#&gt; ERR519509     1  0.1556      0.883 0.920  0 0.000 0.000 0.000 0.080
#&gt; ERR519472     6  0.1845      0.766 0.052  0 0.000 0.000 0.028 0.920
#&gt; ERR519510     5  0.0000      0.753 0.000  0 0.000 0.000 1.000 0.000
#&gt; ERR519470     1  0.0000      0.899 1.000  0 0.000 0.000 0.000 0.000
#&gt; ERR519495     1  0.3198      0.582 0.740  0 0.000 0.000 0.000 0.260
#&gt; ERR519522     1  0.1556      0.883 0.920  0 0.000 0.000 0.000 0.080
#&gt; ERR519523     4  0.1584      0.819 0.064  0 0.000 0.928 0.000 0.008
#&gt; ERR519503     1  0.1556      0.883 0.920  0 0.000 0.000 0.000 0.080
#&gt; ERR519471     1  0.0000      0.899 1.000  0 0.000 0.000 0.000 0.000
#&gt; ERR519500     6  0.4034      0.540 0.020  0 0.000 0.328 0.000 0.652
#&gt; ERR519485     1  0.0260      0.897 0.992  0 0.000 0.000 0.000 0.008
#&gt; ERR519476     2  0.0000      1.000 0.000  1 0.000 0.000 0.000 0.000
#&gt; ERR519502     5  0.0146      0.752 0.000  0 0.000 0.000 0.996 0.004
#&gt; ERR519486     5  0.4814      0.284 0.412  0 0.000 0.000 0.532 0.056
#&gt; ERR519478     1  0.1387      0.885 0.932  0 0.000 0.000 0.000 0.068
#&gt; ERR519497     4  0.3607      0.505 0.000  0 0.000 0.652 0.348 0.000
#&gt; ERR519467     1  0.2165      0.834 0.884  0 0.000 0.108 0.000 0.008
#&gt; ERR519489     6  0.3804      0.387 0.000  0 0.000 0.424 0.000 0.576
#&gt; ERR519494     5  0.5702      0.358 0.000  0 0.292 0.000 0.512 0.196
#&gt; ERR519474     6  0.3672      0.710 0.056  0 0.000 0.000 0.168 0.776
#&gt; ERR519505     5  0.0000      0.753 0.000  0 0.000 0.000 1.000 0.000
#&gt; ERR519517     3  0.0000      0.998 0.000  0 1.000 0.000 0.000 0.000
#&gt; ERR519484     5  0.1267      0.724 0.000  0 0.000 0.000 0.940 0.060
#&gt; ERR519498     5  0.1714      0.711 0.000  0 0.000 0.092 0.908 0.000
#&gt; ERR519490     3  0.0000      0.998 0.000  0 1.000 0.000 0.000 0.000
#&gt; ERR519507     6  0.1814      0.758 0.000  0 0.000 0.000 0.100 0.900
#&gt; ERR519511     5  0.0000      0.753 0.000  0 0.000 0.000 1.000 0.000
#&gt; ERR519468     3  0.0260      0.991 0.000  0 0.992 0.000 0.000 0.008
#&gt; ERR519482     3  0.0000      0.998 0.000  0 1.000 0.000 0.000 0.000
#&gt; ERR519475     2  0.0000      1.000 0.000  1 0.000 0.000 0.000 0.000
#&gt; ERR519496     1  0.0000      0.899 1.000  0 0.000 0.000 0.000 0.000
#&gt; ERR519506     6  0.3869      0.723 0.100  0 0.000 0.000 0.128 0.772
#&gt; ERR519469     6  0.1926      0.762 0.068  0 0.000 0.000 0.020 0.912
#&gt; ERR519480     3  0.0000      0.998 0.000  0 1.000 0.000 0.000 0.000
#&gt; ERR519487     3  0.0000      0.998 0.000  0 1.000 0.000 0.000 0.000
#&gt; ERR519483     1  0.2118      0.827 0.888  0 0.000 0.000 0.008 0.104
#&gt; ERR519477     2  0.0000      1.000 0.000  1 0.000 0.000 0.000 0.000
#&gt; ERR519499     3  0.0000      0.998 0.000  0 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-5-a').click(function(){
  $('#tab-SD-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-pam-membership-heatmap'>
<ul>
<li><a href='#tab-SD-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-pam-get-signatures'>
<ul>
<li><a href='#tab-SD-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-1-1.png" alt="plot of chunk tab-SD-pam-get-signatures-1"/></p>

</div>
<div id='tab-SD-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-2-1.png" alt="plot of chunk tab-SD-pam-get-signatures-2"/></p>

</div>
<div id='tab-SD-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-3-1.png" alt="plot of chunk tab-SD-pam-get-signatures-3"/></p>

</div>
<div id='tab-SD-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-4-1.png" alt="plot of chunk tab-SD-pam-get-signatures-4"/></p>

</div>
<div id='tab-SD-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-5-1.png" alt="plot of chunk tab-SD-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-pam-signature_compare](figure_cola/SD-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-pam-dimension-reduction'>
<ul>
<li><a href='#tab-SD-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-pam-collect-classes](figure_cola/SD-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:mclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "mclust"]
# you can also extract it by
# res = res_list["SD:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 18140 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-mclust-collect-plots](figure_cola/SD-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-mclust-select-partition-number](figure_cola/SD-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.1117 0.889   0.889
#> 3 3 0.344           0.664       0.804         2.8877 0.706   0.669
#> 4 4 0.475           0.826       0.849         0.4174 0.767   0.623
#> 5 5 0.528           0.764       0.840         0.0915 0.928   0.833
#> 6 6 0.540           0.667       0.728         0.1486 0.720   0.343
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-get-classes'>
<ul>
<li><a href='#tab-SD-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-mclust-get-classes-1'>
<p><a id='tab-SD-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette p1 p2
#&gt; ERR519515     1       0          1  1  0
#&gt; ERR519516     1       0          1  1  0
#&gt; ERR519520     1       0          1  1  0
#&gt; ERR519513     1       0          1  1  0
#&gt; ERR519481     1       0          1  1  0
#&gt; ERR519491     1       0          1  1  0
#&gt; ERR519473     1       0          1  1  0
#&gt; ERR519518     1       0          1  1  0
#&gt; ERR519512     1       0          1  1  0
#&gt; ERR519521     1       0          1  1  0
#&gt; ERR519488     1       0          1  1  0
#&gt; ERR519493     1       0          1  1  0
#&gt; ERR519514     1       0          1  1  0
#&gt; ERR519479     1       0          1  1  0
#&gt; ERR519509     1       0          1  1  0
#&gt; ERR519472     1       0          1  1  0
#&gt; ERR519510     1       0          1  1  0
#&gt; ERR519470     1       0          1  1  0
#&gt; ERR519495     1       0          1  1  0
#&gt; ERR519522     1       0          1  1  0
#&gt; ERR519523     1       0          1  1  0
#&gt; ERR519503     1       0          1  1  0
#&gt; ERR519471     1       0          1  1  0
#&gt; ERR519500     1       0          1  1  0
#&gt; ERR519485     1       0          1  1  0
#&gt; ERR519476     2       0          1  0  1
#&gt; ERR519502     1       0          1  1  0
#&gt; ERR519486     1       0          1  1  0
#&gt; ERR519478     1       0          1  1  0
#&gt; ERR519497     1       0          1  1  0
#&gt; ERR519467     1       0          1  1  0
#&gt; ERR519489     1       0          1  1  0
#&gt; ERR519494     1       0          1  1  0
#&gt; ERR519474     1       0          1  1  0
#&gt; ERR519505     1       0          1  1  0
#&gt; ERR519517     1       0          1  1  0
#&gt; ERR519484     1       0          1  1  0
#&gt; ERR519498     1       0          1  1  0
#&gt; ERR519490     1       0          1  1  0
#&gt; ERR519507     1       0          1  1  0
#&gt; ERR519511     1       0          1  1  0
#&gt; ERR519468     1       0          1  1  0
#&gt; ERR519482     1       0          1  1  0
#&gt; ERR519475     2       0          1  0  1
#&gt; ERR519496     1       0          1  1  0
#&gt; ERR519506     1       0          1  1  0
#&gt; ERR519469     1       0          1  1  0
#&gt; ERR519480     1       0          1  1  0
#&gt; ERR519487     1       0          1  1  0
#&gt; ERR519483     1       0          1  1  0
#&gt; ERR519477     2       0          1  0  1
#&gt; ERR519499     1       0          1  1  0
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-1-a').click(function(){
  $('#tab-SD-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-2'>
<p><a id='tab-SD-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3
#&gt; ERR519515     1  0.0424      0.665 0.992  0 0.008
#&gt; ERR519516     1  0.0892      0.654 0.980  0 0.020
#&gt; ERR519520     1  0.4702      0.746 0.788  0 0.212
#&gt; ERR519513     1  0.5760      0.680 0.672  0 0.328
#&gt; ERR519481     3  0.6026      0.651 0.376  0 0.624
#&gt; ERR519491     1  0.0892      0.654 0.980  0 0.020
#&gt; ERR519473     3  0.5988      0.665 0.368  0 0.632
#&gt; ERR519518     1  0.4702      0.746 0.788  0 0.212
#&gt; ERR519512     1  0.4702      0.746 0.788  0 0.212
#&gt; ERR519521     1  0.4702      0.746 0.788  0 0.212
#&gt; ERR519488     1  0.4291      0.743 0.820  0 0.180
#&gt; ERR519493     1  0.0892      0.654 0.980  0 0.020
#&gt; ERR519514     1  0.0892      0.654 0.980  0 0.020
#&gt; ERR519479     3  0.6111      0.748 0.396  0 0.604
#&gt; ERR519509     1  0.4291      0.743 0.820  0 0.180
#&gt; ERR519472     3  0.6111      0.748 0.396  0 0.604
#&gt; ERR519510     3  0.6299      0.713 0.476  0 0.524
#&gt; ERR519470     1  0.1411      0.691 0.964  0 0.036
#&gt; ERR519495     3  0.6126      0.743 0.400  0 0.600
#&gt; ERR519522     1  0.4178      0.743 0.828  0 0.172
#&gt; ERR519523     1  0.1529      0.690 0.960  0 0.040
#&gt; ERR519503     1  0.4702      0.746 0.788  0 0.212
#&gt; ERR519471     1  0.0747      0.658 0.984  0 0.016
#&gt; ERR519500     1  0.6244     -0.617 0.560  0 0.440
#&gt; ERR519485     1  0.0424      0.665 0.992  0 0.008
#&gt; ERR519476     2  0.0000      1.000 0.000  1 0.000
#&gt; ERR519502     3  0.6008      0.669 0.372  0 0.628
#&gt; ERR519486     1  0.0892      0.654 0.980  0 0.020
#&gt; ERR519478     1  0.4121      0.738 0.832  0 0.168
#&gt; ERR519497     1  0.4842      0.746 0.776  0 0.224
#&gt; ERR519467     1  0.3482      0.736 0.872  0 0.128
#&gt; ERR519489     1  0.1964      0.687 0.944  0 0.056
#&gt; ERR519494     1  0.6126      0.626 0.600  0 0.400
#&gt; ERR519474     1  0.5926     -0.410 0.644  0 0.356
#&gt; ERR519505     1  0.4702      0.746 0.788  0 0.212
#&gt; ERR519517     1  0.6126      0.626 0.600  0 0.400
#&gt; ERR519484     3  0.5988      0.665 0.368  0 0.632
#&gt; ERR519498     1  0.4702      0.746 0.788  0 0.212
#&gt; ERR519490     1  0.6126      0.626 0.600  0 0.400
#&gt; ERR519507     3  0.5058      0.732 0.244  0 0.756
#&gt; ERR519511     3  0.6026      0.756 0.376  0 0.624
#&gt; ERR519468     1  0.6062      0.639 0.616  0 0.384
#&gt; ERR519482     1  0.6126      0.626 0.600  0 0.400
#&gt; ERR519475     2  0.0000      1.000 0.000  1 0.000
#&gt; ERR519496     1  0.1031      0.649 0.976  0 0.024
#&gt; ERR519506     1  0.4178      0.743 0.828  0 0.172
#&gt; ERR519469     1  0.1753      0.631 0.952  0 0.048
#&gt; ERR519480     1  0.6126      0.626 0.600  0 0.400
#&gt; ERR519487     1  0.6126      0.626 0.600  0 0.400
#&gt; ERR519483     1  0.4121      0.742 0.832  0 0.168
#&gt; ERR519477     2  0.0000      1.000 0.000  1 0.000
#&gt; ERR519499     1  0.6126      0.626 0.600  0 0.400
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-2-a').click(function(){
  $('#tab-SD-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-3'>
<p><a id='tab-SD-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3    p4
#&gt; ERR519515     1  0.0000      0.784 1.000  0 0.000 0.000
#&gt; ERR519516     1  0.2921      0.801 0.860  0 0.000 0.140
#&gt; ERR519520     1  0.4332      0.758 0.800  0 0.160 0.040
#&gt; ERR519513     3  0.2011      0.879 0.000  0 0.920 0.080
#&gt; ERR519481     4  0.2759      0.906 0.052  0 0.044 0.904
#&gt; ERR519491     1  0.2345      0.803 0.900  0 0.000 0.100
#&gt; ERR519473     4  0.2840      0.909 0.056  0 0.044 0.900
#&gt; ERR519518     1  0.6723      0.726 0.600  0 0.260 0.140
#&gt; ERR519512     1  0.6324      0.783 0.660  0 0.168 0.172
#&gt; ERR519521     1  0.6531      0.769 0.636  0 0.204 0.160
#&gt; ERR519488     1  0.4244      0.761 0.804  0 0.160 0.036
#&gt; ERR519493     1  0.2921      0.801 0.860  0 0.000 0.140
#&gt; ERR519514     1  0.1211      0.791 0.960  0 0.000 0.040
#&gt; ERR519479     4  0.1867      0.892 0.072  0 0.000 0.928
#&gt; ERR519509     1  0.3803      0.779 0.836  0 0.132 0.032
#&gt; ERR519472     4  0.2011      0.889 0.080  0 0.000 0.920
#&gt; ERR519510     4  0.4661      0.506 0.348  0 0.000 0.652
#&gt; ERR519470     1  0.0469      0.782 0.988  0 0.000 0.012
#&gt; ERR519495     1  0.4817      0.590 0.612  0 0.000 0.388
#&gt; ERR519522     1  0.3335      0.786 0.856  0 0.128 0.016
#&gt; ERR519523     1  0.3790      0.798 0.820  0 0.016 0.164
#&gt; ERR519503     1  0.4332      0.758 0.800  0 0.160 0.040
#&gt; ERR519471     1  0.1211      0.791 0.960  0 0.000 0.040
#&gt; ERR519500     1  0.4500      0.615 0.684  0 0.000 0.316
#&gt; ERR519485     1  0.3356      0.799 0.824  0 0.000 0.176
#&gt; ERR519476     2  0.0000      1.000 0.000  1 0.000 0.000
#&gt; ERR519502     4  0.2996      0.883 0.044  0 0.064 0.892
#&gt; ERR519486     1  0.2921      0.801 0.860  0 0.000 0.140
#&gt; ERR519478     1  0.3166      0.788 0.868  0 0.116 0.016
#&gt; ERR519497     1  0.6531      0.769 0.636  0 0.204 0.160
#&gt; ERR519467     1  0.1677      0.793 0.948  0 0.040 0.012
#&gt; ERR519489     1  0.5355      0.810 0.736  0 0.084 0.180
#&gt; ERR519494     3  0.1940      0.899 0.000  0 0.924 0.076
#&gt; ERR519474     1  0.3975      0.769 0.760  0 0.000 0.240
#&gt; ERR519505     1  0.6275      0.778 0.660  0 0.204 0.136
#&gt; ERR519517     3  0.1022      0.949 0.000  0 0.968 0.032
#&gt; ERR519484     4  0.2840      0.909 0.056  0 0.044 0.900
#&gt; ERR519498     1  0.6531      0.769 0.636  0 0.204 0.160
#&gt; ERR519490     3  0.0592      0.940 0.000  0 0.984 0.016
#&gt; ERR519507     4  0.2751      0.910 0.056  0 0.040 0.904
#&gt; ERR519511     4  0.2450      0.901 0.072  0 0.016 0.912
#&gt; ERR519468     3  0.1118      0.931 0.000  0 0.964 0.036
#&gt; ERR519482     3  0.0000      0.946 0.000  0 1.000 0.000
#&gt; ERR519475     2  0.0000      1.000 0.000  1 0.000 0.000
#&gt; ERR519496     1  0.2921      0.801 0.860  0 0.000 0.140
#&gt; ERR519506     1  0.5615      0.785 0.716  0 0.096 0.188
#&gt; ERR519469     1  0.4500      0.719 0.684  0 0.000 0.316
#&gt; ERR519480     3  0.1022      0.949 0.000  0 0.968 0.032
#&gt; ERR519487     3  0.1022      0.949 0.000  0 0.968 0.032
#&gt; ERR519483     1  0.5144      0.793 0.732  0 0.052 0.216
#&gt; ERR519477     2  0.0000      1.000 0.000  1 0.000 0.000
#&gt; ERR519499     3  0.1022      0.949 0.000  0 0.968 0.032
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-3-a').click(function(){
  $('#tab-SD-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-4'>
<p><a id='tab-SD-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3    p4    p5
#&gt; ERR519515     1  0.3912      0.610 0.752  0 0.000 0.020 0.228
#&gt; ERR519516     1  0.1549      0.751 0.944  0 0.000 0.016 0.040
#&gt; ERR519520     1  0.4804      0.700 0.704  0 0.040 0.012 0.244
#&gt; ERR519513     3  0.3452      0.850 0.060  0 0.860 0.036 0.044
#&gt; ERR519481     4  0.1549      0.790 0.040  0 0.016 0.944 0.000
#&gt; ERR519491     1  0.1800      0.751 0.932  0 0.000 0.020 0.048
#&gt; ERR519473     4  0.0963      0.794 0.036  0 0.000 0.964 0.000
#&gt; ERR519518     1  0.5715      0.660 0.672  0 0.216 0.048 0.064
#&gt; ERR519512     1  0.5270      0.710 0.704  0 0.040 0.048 0.208
#&gt; ERR519521     1  0.5637      0.701 0.704  0 0.144 0.048 0.104
#&gt; ERR519488     5  0.1341      1.000 0.056  0 0.000 0.000 0.944
#&gt; ERR519493     1  0.1648      0.751 0.940  0 0.000 0.020 0.040
#&gt; ERR519514     1  0.2012      0.750 0.920  0 0.000 0.020 0.060
#&gt; ERR519479     4  0.3368      0.792 0.156  0 0.000 0.820 0.024
#&gt; ERR519509     5  0.1341      1.000 0.056  0 0.000 0.000 0.944
#&gt; ERR519472     4  0.3602      0.776 0.180  0 0.000 0.796 0.024
#&gt; ERR519510     1  0.4338      0.620 0.696  0 0.000 0.280 0.024
#&gt; ERR519470     1  0.4675      0.496 0.600  0 0.000 0.020 0.380
#&gt; ERR519495     1  0.3197      0.728 0.836  0 0.000 0.140 0.024
#&gt; ERR519522     1  0.4437      0.418 0.532  0 0.004 0.000 0.464
#&gt; ERR519523     1  0.2387      0.770 0.908  0 0.004 0.040 0.048
#&gt; ERR519503     1  0.4900      0.403 0.512  0 0.024 0.000 0.464
#&gt; ERR519471     1  0.2079      0.748 0.916  0 0.000 0.020 0.064
#&gt; ERR519500     1  0.2653      0.742 0.880  0 0.000 0.096 0.024
#&gt; ERR519485     1  0.1648      0.751 0.940  0 0.000 0.020 0.040
#&gt; ERR519476     2  0.0000      1.000 0.000  1 0.000 0.000 0.000
#&gt; ERR519502     4  0.2193      0.778 0.044  0 0.028 0.920 0.008
#&gt; ERR519486     1  0.0898      0.763 0.972  0 0.000 0.008 0.020
#&gt; ERR519478     1  0.4696      0.442 0.556  0 0.000 0.016 0.428
#&gt; ERR519497     1  0.5495      0.690 0.704  0 0.180 0.048 0.068
#&gt; ERR519467     1  0.3039      0.735 0.808  0 0.000 0.000 0.192
#&gt; ERR519489     1  0.3450      0.765 0.848  0 0.008 0.060 0.084
#&gt; ERR519494     3  0.2591      0.906 0.032  0 0.904 0.020 0.044
#&gt; ERR519474     1  0.2900      0.740 0.864  0 0.000 0.108 0.028
#&gt; ERR519505     1  0.5484      0.690 0.704  0 0.180 0.044 0.072
#&gt; ERR519517     3  0.0404      0.927 0.000  0 0.988 0.000 0.012
#&gt; ERR519484     4  0.1205      0.797 0.040  0 0.004 0.956 0.000
#&gt; ERR519498     1  0.5495      0.690 0.704  0 0.180 0.048 0.068
#&gt; ERR519490     3  0.1569      0.929 0.008  0 0.944 0.004 0.044
#&gt; ERR519507     4  0.3152      0.800 0.136  0 0.000 0.840 0.024
#&gt; ERR519511     4  0.4608      0.517 0.336  0 0.000 0.640 0.024
#&gt; ERR519468     3  0.2278      0.916 0.008  0 0.916 0.032 0.044
#&gt; ERR519482     3  0.1412      0.931 0.008  0 0.952 0.004 0.036
#&gt; ERR519475     2  0.0000      1.000 0.000  1 0.000 0.000 0.000
#&gt; ERR519496     1  0.1331      0.757 0.952  0 0.000 0.008 0.040
#&gt; ERR519506     1  0.5237      0.716 0.724  0 0.044 0.172 0.060
#&gt; ERR519469     1  0.4370      0.667 0.724  0 0.000 0.236 0.040
#&gt; ERR519480     3  0.0290      0.926 0.000  0 0.992 0.000 0.008
#&gt; ERR519487     3  0.0290      0.926 0.000  0 0.992 0.000 0.008
#&gt; ERR519483     1  0.4816      0.722 0.748  0 0.024 0.168 0.060
#&gt; ERR519477     2  0.0000      1.000 0.000  1 0.000 0.000 0.000
#&gt; ERR519499     3  0.0290      0.926 0.000  0 0.992 0.000 0.008
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-4-a').click(function(){
  $('#tab-SD-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-5'>
<p><a id='tab-SD-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3    p4    p5    p6
#&gt; ERR519515     1  0.2302      0.736 0.872  0 0.000 0.008 0.000 0.120
#&gt; ERR519516     1  0.0820      0.819 0.972  0 0.000 0.012 0.016 0.000
#&gt; ERR519520     4  0.3667      0.697 0.132  0 0.000 0.788 0.000 0.080
#&gt; ERR519513     4  0.3421      0.528 0.000  0 0.116 0.824 0.016 0.044
#&gt; ERR519481     5  0.3702      0.550 0.000  0 0.004 0.264 0.720 0.012
#&gt; ERR519491     1  0.1049      0.822 0.960  0 0.000 0.008 0.000 0.032
#&gt; ERR519473     5  0.3454      0.581 0.000  0 0.004 0.224 0.760 0.012
#&gt; ERR519518     4  0.3755      0.651 0.052  0 0.112 0.812 0.016 0.008
#&gt; ERR519512     4  0.3455      0.717 0.144  0 0.000 0.800 0.000 0.056
#&gt; ERR519521     4  0.2755      0.736 0.140  0 0.004 0.844 0.000 0.012
#&gt; ERR519488     6  0.1480      0.729 0.020  0 0.000 0.040 0.000 0.940
#&gt; ERR519493     1  0.0820      0.819 0.972  0 0.000 0.012 0.016 0.000
#&gt; ERR519514     1  0.0632      0.822 0.976  0 0.000 0.000 0.000 0.024
#&gt; ERR519479     5  0.2118      0.726 0.104  0 0.000 0.008 0.888 0.000
#&gt; ERR519509     6  0.1644      0.736 0.028  0 0.000 0.040 0.000 0.932
#&gt; ERR519472     5  0.2257      0.730 0.116  0 0.000 0.008 0.876 0.000
#&gt; ERR519510     5  0.3206      0.717 0.152  0 0.000 0.028 0.816 0.004
#&gt; ERR519470     1  0.3168      0.656 0.792  0 0.000 0.016 0.000 0.192
#&gt; ERR519495     5  0.3979      0.652 0.256  0 0.000 0.028 0.712 0.004
#&gt; ERR519522     6  0.4831      0.595 0.096  0 0.000 0.268 0.000 0.636
#&gt; ERR519523     4  0.4628      0.643 0.312  0 0.000 0.632 0.052 0.004
#&gt; ERR519503     6  0.3511      0.732 0.024  0 0.000 0.216 0.000 0.760
#&gt; ERR519471     1  0.0632      0.822 0.976  0 0.000 0.000 0.000 0.024
#&gt; ERR519500     5  0.4617      0.537 0.324  0 0.000 0.048 0.624 0.004
#&gt; ERR519485     1  0.0622      0.822 0.980  0 0.000 0.012 0.008 0.000
#&gt; ERR519476     2  0.0000      1.000 0.000  1 0.000 0.000 0.000 0.000
#&gt; ERR519502     5  0.3608      0.541 0.000  0 0.000 0.272 0.716 0.012
#&gt; ERR519486     1  0.4246     -0.142 0.580  0 0.000 0.400 0.020 0.000
#&gt; ERR519478     1  0.3905      0.435 0.668  0 0.000 0.016 0.000 0.316
#&gt; ERR519497     4  0.3900      0.745 0.136  0 0.056 0.788 0.020 0.000
#&gt; ERR519467     4  0.5292      0.488 0.372  0 0.000 0.520 0.000 0.108
#&gt; ERR519489     4  0.4409      0.721 0.212  0 0.000 0.716 0.060 0.012
#&gt; ERR519494     4  0.4741     -0.323 0.000  0 0.420 0.536 0.004 0.040
#&gt; ERR519474     5  0.6063      0.218 0.368  0 0.000 0.216 0.412 0.004
#&gt; ERR519505     4  0.4502      0.735 0.140  0 0.100 0.740 0.020 0.000
#&gt; ERR519517     3  0.0865      0.777 0.000  0 0.964 0.036 0.000 0.000
#&gt; ERR519484     5  0.3398      0.588 0.000  0 0.004 0.216 0.768 0.012
#&gt; ERR519498     4  0.3965      0.743 0.132  0 0.052 0.792 0.016 0.008
#&gt; ERR519490     3  0.4493      0.708 0.000  0 0.612 0.344 0.000 0.044
#&gt; ERR519507     5  0.2006      0.723 0.104  0 0.004 0.000 0.892 0.000
#&gt; ERR519511     5  0.2553      0.730 0.144  0 0.000 0.008 0.848 0.000
#&gt; ERR519468     3  0.4686      0.692 0.000  0 0.588 0.364 0.004 0.044
#&gt; ERR519482     3  0.4424      0.718 0.000  0 0.632 0.324 0.000 0.044
#&gt; ERR519475     2  0.0000      1.000 0.000  1 0.000 0.000 0.000 0.000
#&gt; ERR519496     1  0.1391      0.800 0.944  0 0.000 0.016 0.040 0.000
#&gt; ERR519506     4  0.5444      0.656 0.204  0 0.000 0.616 0.168 0.012
#&gt; ERR519469     4  0.5269      0.571 0.156  0 0.000 0.596 0.248 0.000
#&gt; ERR519480     3  0.0363      0.775 0.000  0 0.988 0.012 0.000 0.000
#&gt; ERR519487     3  0.0146      0.772 0.000  0 0.996 0.004 0.000 0.000
#&gt; ERR519483     4  0.5381      0.649 0.204  0 0.000 0.616 0.172 0.008
#&gt; ERR519477     2  0.0000      1.000 0.000  1 0.000 0.000 0.000 0.000
#&gt; ERR519499     3  0.0146      0.772 0.000  0 0.996 0.004 0.000 0.000
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-5-a').click(function(){
  $('#tab-SD-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-SD-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-get-signatures'>
<ul>
<li><a href='#tab-SD-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-1-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-1"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-2-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-2"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-3-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-3"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-4-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-4"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-5-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-mclust-signature_compare](figure_cola/SD-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-SD-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-mclust-collect-classes](figure_cola/SD-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:NMF






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "NMF"]
# you can also extract it by
# res = res_list["SD:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 18140 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-NMF-collect-plots](figure_cola/SD-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-NMF-select-partition-number](figure_cola/SD-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.701           0.882       0.946         0.4570 0.538   0.538
#> 3 3 0.450           0.590       0.805         0.4035 0.619   0.394
#> 4 4 0.440           0.594       0.741         0.1449 0.825   0.538
#> 5 5 0.526           0.472       0.724         0.0629 0.921   0.703
#> 6 6 0.593           0.458       0.700         0.0345 0.914   0.650
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-get-classes'>
<ul>
<li><a href='#tab-SD-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-NMF-get-classes-1'>
<p><a id='tab-SD-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; ERR519515     1   0.000      0.950 1.000 0.000
#&gt; ERR519516     1   0.000      0.950 1.000 0.000
#&gt; ERR519520     1   0.000      0.950 1.000 0.000
#&gt; ERR519513     2   0.000      0.915 0.000 1.000
#&gt; ERR519481     2   0.745      0.777 0.212 0.788
#&gt; ERR519491     1   0.000      0.950 1.000 0.000
#&gt; ERR519473     2   0.163      0.909 0.024 0.976
#&gt; ERR519518     2   0.000      0.915 0.000 1.000
#&gt; ERR519512     1   0.000      0.950 1.000 0.000
#&gt; ERR519521     1   0.634      0.792 0.840 0.160
#&gt; ERR519488     1   0.000      0.950 1.000 0.000
#&gt; ERR519493     1   0.000      0.950 1.000 0.000
#&gt; ERR519514     1   0.000      0.950 1.000 0.000
#&gt; ERR519479     1   0.000      0.950 1.000 0.000
#&gt; ERR519509     1   0.000      0.950 1.000 0.000
#&gt; ERR519472     1   0.000      0.950 1.000 0.000
#&gt; ERR519510     1   0.388      0.890 0.924 0.076
#&gt; ERR519470     1   0.000      0.950 1.000 0.000
#&gt; ERR519495     1   0.000      0.950 1.000 0.000
#&gt; ERR519522     1   0.000      0.950 1.000 0.000
#&gt; ERR519523     1   0.000      0.950 1.000 0.000
#&gt; ERR519503     1   0.000      0.950 1.000 0.000
#&gt; ERR519471     1   0.000      0.950 1.000 0.000
#&gt; ERR519500     1   0.000      0.950 1.000 0.000
#&gt; ERR519485     1   0.000      0.950 1.000 0.000
#&gt; ERR519476     1   0.000      0.950 1.000 0.000
#&gt; ERR519502     2   0.615      0.835 0.152 0.848
#&gt; ERR519486     1   0.000      0.950 1.000 0.000
#&gt; ERR519478     1   0.000      0.950 1.000 0.000
#&gt; ERR519497     2   0.738      0.781 0.208 0.792
#&gt; ERR519467     1   0.000      0.950 1.000 0.000
#&gt; ERR519489     1   0.518      0.846 0.884 0.116
#&gt; ERR519494     2   0.000      0.915 0.000 1.000
#&gt; ERR519474     1   0.000      0.950 1.000 0.000
#&gt; ERR519505     2   0.913      0.571 0.328 0.672
#&gt; ERR519517     2   0.000      0.915 0.000 1.000
#&gt; ERR519484     2   0.689      0.808 0.184 0.816
#&gt; ERR519498     2   0.204      0.906 0.032 0.968
#&gt; ERR519490     2   0.000      0.915 0.000 1.000
#&gt; ERR519507     1   0.224      0.924 0.964 0.036
#&gt; ERR519511     1   0.767      0.695 0.776 0.224
#&gt; ERR519468     2   0.000      0.915 0.000 1.000
#&gt; ERR519482     2   0.000      0.915 0.000 1.000
#&gt; ERR519475     1   0.891      0.534 0.692 0.308
#&gt; ERR519496     1   0.000      0.950 1.000 0.000
#&gt; ERR519506     1   0.163      0.934 0.976 0.024
#&gt; ERR519469     1   0.991      0.138 0.556 0.444
#&gt; ERR519480     2   0.000      0.915 0.000 1.000
#&gt; ERR519487     2   0.000      0.915 0.000 1.000
#&gt; ERR519483     1   0.456      0.868 0.904 0.096
#&gt; ERR519477     2   0.722      0.777 0.200 0.800
#&gt; ERR519499     2   0.000      0.915 0.000 1.000
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-1-a').click(function(){
  $('#tab-SD-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-2'>
<p><a id='tab-SD-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; ERR519515     2  0.1031     0.8006 0.024 0.976 0.000
#&gt; ERR519516     1  0.6026     0.4378 0.624 0.376 0.000
#&gt; ERR519520     2  0.0000     0.7976 0.000 1.000 0.000
#&gt; ERR519513     1  0.6302    -0.4454 0.520 0.000 0.480
#&gt; ERR519481     1  0.0237     0.7160 0.996 0.000 0.004
#&gt; ERR519491     2  0.5497     0.5119 0.292 0.708 0.000
#&gt; ERR519473     1  0.0000     0.7192 1.000 0.000 0.000
#&gt; ERR519518     3  0.6140     0.6334 0.404 0.000 0.596
#&gt; ERR519512     2  0.0747     0.8006 0.016 0.984 0.000
#&gt; ERR519521     1  0.2446     0.7293 0.936 0.052 0.012
#&gt; ERR519488     2  0.0000     0.7976 0.000 1.000 0.000
#&gt; ERR519493     1  0.6008     0.4475 0.628 0.372 0.000
#&gt; ERR519514     2  0.2261     0.7840 0.068 0.932 0.000
#&gt; ERR519479     1  0.1860     0.7376 0.948 0.052 0.000
#&gt; ERR519509     2  0.0000     0.7976 0.000 1.000 0.000
#&gt; ERR519472     1  0.4452     0.6920 0.808 0.192 0.000
#&gt; ERR519510     1  0.1529     0.7351 0.960 0.040 0.000
#&gt; ERR519470     2  0.1163     0.8001 0.028 0.972 0.000
#&gt; ERR519495     1  0.5397     0.6061 0.720 0.280 0.000
#&gt; ERR519522     2  0.0237     0.7991 0.004 0.996 0.000
#&gt; ERR519523     2  0.5968     0.3524 0.364 0.636 0.000
#&gt; ERR519503     2  0.5098     0.5345 0.000 0.752 0.248
#&gt; ERR519471     2  0.2356     0.7817 0.072 0.928 0.000
#&gt; ERR519500     1  0.5529     0.5847 0.704 0.296 0.000
#&gt; ERR519485     2  0.6280     0.0368 0.460 0.540 0.000
#&gt; ERR519476     2  0.8345     0.3077 0.096 0.560 0.344
#&gt; ERR519502     1  0.0237     0.7160 0.996 0.000 0.004
#&gt; ERR519486     2  0.5650     0.4730 0.312 0.688 0.000
#&gt; ERR519478     2  0.0237     0.7991 0.004 0.996 0.000
#&gt; ERR519497     3  0.7413     0.6983 0.204 0.104 0.692
#&gt; ERR519467     2  0.1163     0.8001 0.028 0.972 0.000
#&gt; ERR519489     1  0.5678     0.5674 0.684 0.316 0.000
#&gt; ERR519494     1  0.6299    -0.4442 0.524 0.000 0.476
#&gt; ERR519474     1  0.5760     0.5332 0.672 0.328 0.000
#&gt; ERR519505     2  0.9778    -0.3213 0.236 0.408 0.356
#&gt; ERR519517     3  0.2066     0.7443 0.060 0.000 0.940
#&gt; ERR519484     1  0.0000     0.7192 1.000 0.000 0.000
#&gt; ERR519498     3  0.6205     0.7061 0.336 0.008 0.656
#&gt; ERR519490     3  0.5138     0.7481 0.252 0.000 0.748
#&gt; ERR519507     1  0.0000     0.7192 1.000 0.000 0.000
#&gt; ERR519511     1  0.0237     0.7160 0.996 0.000 0.004
#&gt; ERR519468     3  0.5859     0.6989 0.344 0.000 0.656
#&gt; ERR519482     3  0.5591     0.7272 0.304 0.000 0.696
#&gt; ERR519475     3  0.8865    -0.0455 0.120 0.404 0.476
#&gt; ERR519496     2  0.2537     0.7759 0.080 0.920 0.000
#&gt; ERR519506     1  0.3482     0.7290 0.872 0.128 0.000
#&gt; ERR519469     1  0.1031     0.7309 0.976 0.024 0.000
#&gt; ERR519480     3  0.2625     0.7522 0.084 0.000 0.916
#&gt; ERR519487     3  0.3482     0.7583 0.128 0.000 0.872
#&gt; ERR519483     1  0.4702     0.6776 0.788 0.212 0.000
#&gt; ERR519477     3  0.8677     0.4972 0.288 0.140 0.572
#&gt; ERR519499     3  0.0000     0.7121 0.000 0.000 1.000
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-2-a').click(function(){
  $('#tab-SD-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-3'>
<p><a id='tab-SD-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; ERR519515     1  0.1004    0.81739 0.972 0.004 0.000 0.024
#&gt; ERR519516     2  0.5807    0.49836 0.160 0.708 0.000 0.132
#&gt; ERR519520     1  0.5041    0.64160 0.728 0.232 0.000 0.040
#&gt; ERR519513     2  0.5985    0.53981 0.000 0.692 0.168 0.140
#&gt; ERR519481     4  0.5713    0.23477 0.000 0.360 0.036 0.604
#&gt; ERR519491     1  0.3542    0.75328 0.852 0.120 0.000 0.028
#&gt; ERR519473     4  0.3810    0.57280 0.000 0.092 0.060 0.848
#&gt; ERR519518     3  0.6949    0.24891 0.000 0.348 0.528 0.124
#&gt; ERR519512     1  0.5233    0.51776 0.648 0.332 0.000 0.020
#&gt; ERR519521     2  0.5516    0.51683 0.056 0.732 0.012 0.200
#&gt; ERR519488     1  0.3161    0.77357 0.864 0.124 0.000 0.012
#&gt; ERR519493     2  0.6111    0.44601 0.256 0.652 0.000 0.092
#&gt; ERR519514     1  0.1256    0.81721 0.964 0.008 0.000 0.028
#&gt; ERR519479     4  0.6275    0.50647 0.084 0.272 0.004 0.640
#&gt; ERR519509     1  0.2197    0.80026 0.916 0.080 0.000 0.004
#&gt; ERR519472     4  0.5427    0.68732 0.164 0.100 0.000 0.736
#&gt; ERR519510     2  0.4234    0.63852 0.032 0.840 0.028 0.100
#&gt; ERR519470     1  0.1256    0.81574 0.964 0.008 0.000 0.028
#&gt; ERR519495     4  0.6179    0.64244 0.320 0.072 0.000 0.608
#&gt; ERR519522     1  0.2053    0.80491 0.924 0.072 0.000 0.004
#&gt; ERR519523     1  0.4174    0.70761 0.816 0.140 0.000 0.044
#&gt; ERR519503     1  0.6388    0.62004 0.700 0.048 0.188 0.064
#&gt; ERR519471     1  0.2385    0.79773 0.920 0.028 0.000 0.052
#&gt; ERR519500     4  0.6774    0.57063 0.160 0.196 0.008 0.636
#&gt; ERR519485     1  0.4332    0.68684 0.800 0.040 0.000 0.160
#&gt; ERR519476     2  0.9867    0.05344 0.264 0.316 0.184 0.236
#&gt; ERR519502     2  0.5199    0.61219 0.024 0.768 0.040 0.168
#&gt; ERR519486     1  0.5925    0.46567 0.648 0.284 0.000 0.068
#&gt; ERR519478     1  0.0336    0.82058 0.992 0.008 0.000 0.000
#&gt; ERR519497     2  0.4692    0.51594 0.020 0.772 0.196 0.012
#&gt; ERR519467     1  0.0336    0.82069 0.992 0.008 0.000 0.000
#&gt; ERR519489     4  0.6941    0.48270 0.192 0.220 0.000 0.588
#&gt; ERR519494     3  0.7109    0.42717 0.000 0.144 0.520 0.336
#&gt; ERR519474     4  0.6067    0.55375 0.376 0.052 0.000 0.572
#&gt; ERR519505     2  0.3204    0.62417 0.064 0.892 0.028 0.016
#&gt; ERR519517     3  0.0937    0.73359 0.000 0.012 0.976 0.012
#&gt; ERR519484     2  0.6196    0.44352 0.016 0.616 0.040 0.328
#&gt; ERR519498     2  0.3006    0.62632 0.012 0.888 0.092 0.008
#&gt; ERR519490     3  0.3271    0.73153 0.000 0.012 0.856 0.132
#&gt; ERR519507     4  0.5644    0.57221 0.060 0.220 0.008 0.712
#&gt; ERR519511     2  0.6334    0.49273 0.024 0.632 0.044 0.300
#&gt; ERR519468     3  0.4345    0.71179 0.004 0.020 0.788 0.188
#&gt; ERR519482     3  0.4281    0.71659 0.000 0.028 0.792 0.180
#&gt; ERR519475     3  0.9832    0.00532 0.176 0.248 0.328 0.248
#&gt; ERR519496     1  0.2125    0.79039 0.920 0.004 0.000 0.076
#&gt; ERR519506     4  0.4700    0.66633 0.208 0.012 0.016 0.764
#&gt; ERR519469     4  0.4959    0.68050 0.180 0.024 0.024 0.772
#&gt; ERR519480     3  0.1510    0.73022 0.000 0.016 0.956 0.028
#&gt; ERR519487     3  0.2928    0.73213 0.000 0.052 0.896 0.052
#&gt; ERR519483     4  0.5636    0.61662 0.288 0.016 0.024 0.672
#&gt; ERR519477     2  0.8897   -0.08863 0.060 0.368 0.360 0.212
#&gt; ERR519499     3  0.1042    0.71745 0.000 0.008 0.972 0.020
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-3-a').click(function(){
  $('#tab-SD-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-4'>
<p><a id='tab-SD-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; ERR519515     1  0.1310     0.6790 0.956 0.020 0.000 0.024 0.000
#&gt; ERR519516     5  0.6581     0.1408 0.160 0.016 0.000 0.300 0.524
#&gt; ERR519520     1  0.5580     0.4465 0.624 0.068 0.004 0.008 0.296
#&gt; ERR519513     5  0.5742     0.4358 0.000 0.048 0.284 0.040 0.628
#&gt; ERR519481     4  0.3559     0.4880 0.004 0.008 0.004 0.800 0.184
#&gt; ERR519491     1  0.3410     0.6469 0.860 0.024 0.000 0.052 0.064
#&gt; ERR519473     4  0.1679     0.5716 0.016 0.020 0.004 0.948 0.012
#&gt; ERR519518     3  0.7166     0.2400 0.000 0.036 0.452 0.332 0.180
#&gt; ERR519512     1  0.5508     0.4360 0.612 0.060 0.000 0.012 0.316
#&gt; ERR519521     4  0.6405     0.1010 0.080 0.032 0.000 0.476 0.412
#&gt; ERR519488     1  0.3853     0.6315 0.804 0.036 0.000 0.008 0.152
#&gt; ERR519493     5  0.5448     0.3835 0.300 0.008 0.000 0.068 0.624
#&gt; ERR519514     1  0.1865     0.6769 0.936 0.024 0.000 0.032 0.008
#&gt; ERR519479     4  0.4969     0.4152 0.020 0.032 0.000 0.684 0.264
#&gt; ERR519509     1  0.3233     0.6639 0.852 0.028 0.000 0.008 0.112
#&gt; ERR519472     4  0.2589     0.5725 0.048 0.044 0.000 0.900 0.008
#&gt; ERR519510     5  0.3316     0.6004 0.024 0.012 0.016 0.080 0.868
#&gt; ERR519470     1  0.1893     0.6649 0.928 0.048 0.000 0.024 0.000
#&gt; ERR519495     4  0.5711     0.1764 0.356 0.052 0.000 0.572 0.020
#&gt; ERR519522     1  0.2722     0.6721 0.868 0.004 0.000 0.008 0.120
#&gt; ERR519523     1  0.3062     0.6534 0.868 0.004 0.000 0.048 0.080
#&gt; ERR519503     1  0.5810     0.5385 0.712 0.128 0.072 0.008 0.080
#&gt; ERR519471     1  0.4400     0.4557 0.744 0.196 0.000 0.060 0.000
#&gt; ERR519500     4  0.3376     0.5483 0.032 0.012 0.000 0.848 0.108
#&gt; ERR519485     1  0.5991    -0.2594 0.464 0.452 0.000 0.068 0.016
#&gt; ERR519476     2  0.7394     0.3304 0.164 0.580 0.036 0.056 0.164
#&gt; ERR519502     5  0.4645     0.1748 0.008 0.000 0.004 0.424 0.564
#&gt; ERR519486     1  0.7295    -0.0435 0.460 0.156 0.000 0.056 0.328
#&gt; ERR519478     1  0.1369     0.6927 0.956 0.008 0.000 0.008 0.028
#&gt; ERR519497     5  0.5077     0.5402 0.060 0.076 0.072 0.016 0.776
#&gt; ERR519467     1  0.1282     0.6927 0.952 0.000 0.000 0.004 0.044
#&gt; ERR519489     4  0.6513     0.3930 0.096 0.020 0.044 0.640 0.200
#&gt; ERR519494     3  0.5687     0.5801 0.000 0.008 0.620 0.276 0.096
#&gt; ERR519474     2  0.7033     0.2909 0.352 0.392 0.000 0.244 0.012
#&gt; ERR519505     5  0.3124     0.6130 0.004 0.028 0.084 0.012 0.872
#&gt; ERR519517     3  0.0579     0.7948 0.000 0.008 0.984 0.000 0.008
#&gt; ERR519484     5  0.5136     0.3852 0.008 0.016 0.016 0.328 0.632
#&gt; ERR519498     5  0.3788     0.6073 0.004 0.012 0.144 0.024 0.816
#&gt; ERR519490     3  0.4951     0.7039 0.000 0.092 0.744 0.144 0.020
#&gt; ERR519507     4  0.5388     0.5104 0.028 0.104 0.000 0.712 0.156
#&gt; ERR519511     4  0.4947    -0.1388 0.012 0.004 0.004 0.496 0.484
#&gt; ERR519468     3  0.2244     0.7926 0.000 0.024 0.920 0.040 0.016
#&gt; ERR519482     3  0.3959     0.7549 0.000 0.068 0.816 0.104 0.012
#&gt; ERR519475     2  0.6915     0.3497 0.076 0.652 0.080 0.060 0.132
#&gt; ERR519496     1  0.3701     0.5810 0.824 0.112 0.000 0.060 0.004
#&gt; ERR519506     2  0.6756     0.3960 0.300 0.516 0.004 0.164 0.016
#&gt; ERR519469     4  0.6404     0.0774 0.264 0.168 0.012 0.556 0.000
#&gt; ERR519480     3  0.2378     0.7816 0.000 0.048 0.904 0.000 0.048
#&gt; ERR519487     3  0.2275     0.7826 0.000 0.012 0.912 0.012 0.064
#&gt; ERR519483     2  0.6195     0.3305 0.360 0.508 0.004 0.128 0.000
#&gt; ERR519477     2  0.8214     0.1994 0.036 0.492 0.164 0.100 0.208
#&gt; ERR519499     3  0.0579     0.7944 0.000 0.008 0.984 0.000 0.008
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-4-a').click(function(){
  $('#tab-SD-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-5'>
<p><a id='tab-SD-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; ERR519515     1  0.1226     0.6858 0.952 0.004 0.000 0.004 0.000 0.040
#&gt; ERR519516     5  0.7392     0.1054 0.240 0.088 0.000 0.256 0.404 0.012
#&gt; ERR519520     1  0.6197     0.3864 0.544 0.212 0.000 0.016 0.216 0.012
#&gt; ERR519513     5  0.4776     0.2184 0.000 0.028 0.412 0.008 0.548 0.004
#&gt; ERR519481     4  0.3293     0.4179 0.000 0.004 0.004 0.788 0.196 0.008
#&gt; ERR519491     1  0.2757     0.6695 0.884 0.004 0.000 0.024 0.052 0.036
#&gt; ERR519473     4  0.2119     0.5345 0.008 0.004 0.008 0.920 0.016 0.044
#&gt; ERR519518     4  0.7339     0.1186 0.000 0.248 0.128 0.392 0.232 0.000
#&gt; ERR519512     1  0.6492     0.2916 0.500 0.196 0.000 0.020 0.268 0.016
#&gt; ERR519521     4  0.6455     0.2050 0.068 0.088 0.004 0.528 0.304 0.008
#&gt; ERR519488     1  0.2995     0.6728 0.864 0.072 0.000 0.004 0.048 0.012
#&gt; ERR519493     5  0.5091     0.4104 0.248 0.008 0.000 0.048 0.664 0.032
#&gt; ERR519514     1  0.1457     0.6866 0.948 0.004 0.000 0.016 0.004 0.028
#&gt; ERR519479     5  0.6104     0.0853 0.028 0.000 0.000 0.364 0.472 0.136
#&gt; ERR519509     1  0.1989     0.6943 0.916 0.052 0.000 0.004 0.028 0.000
#&gt; ERR519472     4  0.2945     0.5291 0.048 0.004 0.000 0.860 0.004 0.084
#&gt; ERR519510     5  0.1983     0.5344 0.012 0.000 0.012 0.060 0.916 0.000
#&gt; ERR519470     1  0.1411     0.6753 0.936 0.000 0.000 0.004 0.000 0.060
#&gt; ERR519495     1  0.5975    -0.0654 0.480 0.008 0.000 0.376 0.012 0.124
#&gt; ERR519522     1  0.1867     0.6967 0.924 0.036 0.000 0.004 0.036 0.000
#&gt; ERR519523     1  0.2681     0.6782 0.888 0.008 0.000 0.044 0.048 0.012
#&gt; ERR519503     1  0.5900     0.2533 0.496 0.412 0.020 0.016 0.024 0.032
#&gt; ERR519471     1  0.3380     0.4313 0.748 0.004 0.000 0.004 0.000 0.244
#&gt; ERR519500     4  0.2948     0.5245 0.056 0.012 0.000 0.868 0.060 0.004
#&gt; ERR519485     6  0.4636     0.7295 0.336 0.008 0.000 0.020 0.012 0.624
#&gt; ERR519476     2  0.8124     0.4822 0.088 0.368 0.028 0.064 0.100 0.352
#&gt; ERR519502     5  0.4457     0.2169 0.000 0.016 0.008 0.432 0.544 0.000
#&gt; ERR519486     1  0.6497    -0.0232 0.540 0.012 0.020 0.012 0.172 0.244
#&gt; ERR519478     1  0.0914     0.7016 0.968 0.016 0.000 0.000 0.016 0.000
#&gt; ERR519497     5  0.5739     0.3497 0.048 0.272 0.024 0.024 0.620 0.012
#&gt; ERR519467     1  0.1599     0.7021 0.940 0.028 0.000 0.000 0.024 0.008
#&gt; ERR519489     4  0.6130     0.3969 0.068 0.140 0.008 0.636 0.140 0.008
#&gt; ERR519494     3  0.4926     0.5773 0.000 0.032 0.692 0.200 0.076 0.000
#&gt; ERR519474     6  0.4769     0.8217 0.236 0.000 0.000 0.084 0.008 0.672
#&gt; ERR519505     5  0.2930     0.5197 0.000 0.044 0.072 0.004 0.868 0.012
#&gt; ERR519517     3  0.0865     0.7668 0.000 0.036 0.964 0.000 0.000 0.000
#&gt; ERR519484     5  0.4855     0.4590 0.012 0.008 0.012 0.200 0.712 0.056
#&gt; ERR519498     5  0.4922     0.4529 0.008 0.076 0.256 0.004 0.656 0.000
#&gt; ERR519490     2  0.6307    -0.3588 0.000 0.404 0.400 0.176 0.012 0.008
#&gt; ERR519507     4  0.6585     0.0718 0.032 0.000 0.000 0.416 0.316 0.236
#&gt; ERR519511     5  0.4377     0.3795 0.012 0.004 0.000 0.316 0.652 0.016
#&gt; ERR519468     3  0.2168     0.7464 0.000 0.028 0.916 0.004 0.016 0.036
#&gt; ERR519482     3  0.5753     0.3879 0.000 0.264 0.556 0.168 0.012 0.000
#&gt; ERR519475     2  0.7243     0.5045 0.024 0.416 0.056 0.056 0.052 0.396
#&gt; ERR519496     1  0.2963     0.5852 0.828 0.000 0.000 0.016 0.004 0.152
#&gt; ERR519506     6  0.4574     0.7231 0.136 0.004 0.008 0.032 0.060 0.760
#&gt; ERR519469     4  0.7492    -0.3201 0.280 0.020 0.068 0.348 0.000 0.284
#&gt; ERR519480     3  0.3739     0.6596 0.000 0.220 0.752 0.004 0.020 0.004
#&gt; ERR519487     3  0.1405     0.7514 0.000 0.024 0.948 0.000 0.024 0.004
#&gt; ERR519483     6  0.4056     0.8223 0.208 0.008 0.004 0.028 0.004 0.748
#&gt; ERR519477     2  0.8075     0.4822 0.000 0.344 0.140 0.056 0.144 0.316
#&gt; ERR519499     3  0.0891     0.7662 0.000 0.024 0.968 0.000 0.000 0.008
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-5-a').click(function(){
  $('#tab-SD-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-SD-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-get-signatures'>
<ul>
<li><a href='#tab-SD-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-1-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-1"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-2-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-2"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-3-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-3"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-4-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-4"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-5-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-NMF-signature_compare](figure_cola/SD-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-SD-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-NMF-collect-classes](figure_cola/SD-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:hclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "hclust"]
# you can also extract it by
# res = res_list["CV:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 18140 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-hclust-collect-plots](figure_cola/CV-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-hclust-select-partition-number](figure_cola/CV-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.998       0.999         0.2379 0.762   0.762
#> 3 3 1.000           0.979       0.999         0.0259 0.995   0.994
#> 4 4 0.576           0.611       0.869         0.5020 0.967   0.956
#> 5 5 0.468           0.725       0.817         0.1292 1.000   1.000
#> 6 6 0.496           0.695       0.819         0.0470 0.962   0.947
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-get-classes'>
<ul>
<li><a href='#tab-CV-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-hclust-get-classes-1'>
<p><a id='tab-CV-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; ERR519515     1   0.000      1.000 1.000 0.000
#&gt; ERR519516     1   0.000      1.000 1.000 0.000
#&gt; ERR519520     1   0.000      1.000 1.000 0.000
#&gt; ERR519513     1   0.000      1.000 1.000 0.000
#&gt; ERR519481     1   0.000      1.000 1.000 0.000
#&gt; ERR519491     1   0.000      1.000 1.000 0.000
#&gt; ERR519473     1   0.000      1.000 1.000 0.000
#&gt; ERR519518     1   0.000      1.000 1.000 0.000
#&gt; ERR519512     1   0.000      1.000 1.000 0.000
#&gt; ERR519521     1   0.000      1.000 1.000 0.000
#&gt; ERR519488     1   0.000      1.000 1.000 0.000
#&gt; ERR519493     1   0.000      1.000 1.000 0.000
#&gt; ERR519514     1   0.000      1.000 1.000 0.000
#&gt; ERR519479     1   0.000      1.000 1.000 0.000
#&gt; ERR519509     1   0.000      1.000 1.000 0.000
#&gt; ERR519472     1   0.000      1.000 1.000 0.000
#&gt; ERR519510     1   0.000      1.000 1.000 0.000
#&gt; ERR519470     1   0.000      1.000 1.000 0.000
#&gt; ERR519495     1   0.000      1.000 1.000 0.000
#&gt; ERR519522     1   0.000      1.000 1.000 0.000
#&gt; ERR519523     1   0.000      1.000 1.000 0.000
#&gt; ERR519503     1   0.000      1.000 1.000 0.000
#&gt; ERR519471     1   0.000      1.000 1.000 0.000
#&gt; ERR519500     1   0.000      1.000 1.000 0.000
#&gt; ERR519485     1   0.000      1.000 1.000 0.000
#&gt; ERR519476     1   0.000      1.000 1.000 0.000
#&gt; ERR519502     1   0.000      1.000 1.000 0.000
#&gt; ERR519486     1   0.000      1.000 1.000 0.000
#&gt; ERR519478     1   0.000      1.000 1.000 0.000
#&gt; ERR519497     1   0.000      1.000 1.000 0.000
#&gt; ERR519467     1   0.000      1.000 1.000 0.000
#&gt; ERR519489     2   0.000      0.995 0.000 1.000
#&gt; ERR519494     2   0.000      0.995 0.000 1.000
#&gt; ERR519474     1   0.000      1.000 1.000 0.000
#&gt; ERR519505     1   0.000      1.000 1.000 0.000
#&gt; ERR519517     2   0.000      0.995 0.000 1.000
#&gt; ERR519484     1   0.000      1.000 1.000 0.000
#&gt; ERR519498     1   0.000      1.000 1.000 0.000
#&gt; ERR519490     2   0.000      0.995 0.000 1.000
#&gt; ERR519507     1   0.000      1.000 1.000 0.000
#&gt; ERR519511     1   0.000      1.000 1.000 0.000
#&gt; ERR519468     1   0.000      1.000 1.000 0.000
#&gt; ERR519482     1   0.141      0.979 0.980 0.020
#&gt; ERR519475     1   0.000      1.000 1.000 0.000
#&gt; ERR519496     1   0.000      1.000 1.000 0.000
#&gt; ERR519506     1   0.000      1.000 1.000 0.000
#&gt; ERR519469     1   0.000      1.000 1.000 0.000
#&gt; ERR519480     2   0.204      0.967 0.032 0.968
#&gt; ERR519487     2   0.000      0.995 0.000 1.000
#&gt; ERR519483     1   0.000      1.000 1.000 0.000
#&gt; ERR519477     1   0.000      1.000 1.000 0.000
#&gt; ERR519499     2   0.000      0.995 0.000 1.000
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-1-a').click(function(){
  $('#tab-CV-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-2'>
<p><a id='tab-CV-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette   p1   p2 p3
#&gt; ERR519515     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519516     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519520     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519513     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519481     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519491     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519473     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519518     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519512     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519521     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519488     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519493     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519514     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519479     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519509     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519472     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519510     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519470     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519495     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519522     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519523     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519503     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519471     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519500     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519485     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519476     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519502     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519486     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519478     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519497     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519467     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519489     3   0.000      1.000 0.00 0.00  1
#&gt; ERR519494     3   0.000      1.000 0.00 0.00  1
#&gt; ERR519474     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519505     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519517     3   0.000      1.000 0.00 0.00  1
#&gt; ERR519484     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519498     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519490     3   0.000      1.000 0.00 0.00  1
#&gt; ERR519507     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519511     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519468     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519482     1   0.153      0.958 0.96 0.04  0
#&gt; ERR519475     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519496     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519506     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519469     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519480     2   0.000      0.000 0.00 1.00  0
#&gt; ERR519487     3   0.000      1.000 0.00 0.00  1
#&gt; ERR519483     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519477     1   0.000      0.999 1.00 0.00  0
#&gt; ERR519499     3   0.000      1.000 0.00 0.00  1
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-2-a').click(function(){
  $('#tab-CV-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-3'>
<p><a id='tab-CV-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3 p4
#&gt; ERR519515     1  0.0336      0.741 0.992 0.008 0.000  0
#&gt; ERR519516     1  0.0469      0.738 0.988 0.012 0.000  0
#&gt; ERR519520     1  0.0336      0.741 0.992 0.008 0.000  0
#&gt; ERR519513     1  0.1716      0.723 0.936 0.064 0.000  0
#&gt; ERR519481     1  0.3356      0.617 0.824 0.176 0.000  0
#&gt; ERR519491     1  0.0336      0.736 0.992 0.008 0.000  0
#&gt; ERR519473     1  0.4431      0.345 0.696 0.304 0.000  0
#&gt; ERR519518     1  0.4431      0.345 0.696 0.304 0.000  0
#&gt; ERR519512     1  0.0336      0.741 0.992 0.008 0.000  0
#&gt; ERR519521     1  0.3356      0.617 0.824 0.176 0.000  0
#&gt; ERR519488     1  0.0336      0.741 0.992 0.008 0.000  0
#&gt; ERR519493     1  0.0336      0.736 0.992 0.008 0.000  0
#&gt; ERR519514     1  0.0336      0.741 0.992 0.008 0.000  0
#&gt; ERR519479     1  0.3356      0.617 0.824 0.176 0.000  0
#&gt; ERR519509     1  0.0336      0.741 0.992 0.008 0.000  0
#&gt; ERR519472     1  0.4250      0.424 0.724 0.276 0.000  0
#&gt; ERR519510     1  0.1792      0.722 0.932 0.068 0.000  0
#&gt; ERR519470     1  0.0336      0.741 0.992 0.008 0.000  0
#&gt; ERR519495     1  0.4431      0.345 0.696 0.304 0.000  0
#&gt; ERR519522     1  0.0336      0.741 0.992 0.008 0.000  0
#&gt; ERR519523     1  0.0336      0.741 0.992 0.008 0.000  0
#&gt; ERR519503     1  0.4431      0.345 0.696 0.304 0.000  0
#&gt; ERR519471     1  0.0336      0.741 0.992 0.008 0.000  0
#&gt; ERR519500     1  0.3873      0.531 0.772 0.228 0.000  0
#&gt; ERR519485     1  0.4431      0.345 0.696 0.304 0.000  0
#&gt; ERR519476     1  0.0817      0.724 0.976 0.024 0.000  0
#&gt; ERR519502     1  0.3486      0.600 0.812 0.188 0.000  0
#&gt; ERR519486     1  0.4431      0.345 0.696 0.304 0.000  0
#&gt; ERR519478     1  0.0336      0.741 0.992 0.008 0.000  0
#&gt; ERR519497     1  0.4431      0.345 0.696 0.304 0.000  0
#&gt; ERR519467     1  0.0817      0.724 0.976 0.024 0.000  0
#&gt; ERR519489     3  0.1474      0.887 0.000 0.052 0.948  0
#&gt; ERR519494     3  0.0000      0.913 0.000 0.000 1.000  0
#&gt; ERR519474     1  0.0469      0.738 0.988 0.012 0.000  0
#&gt; ERR519505     1  0.0817      0.724 0.976 0.024 0.000  0
#&gt; ERR519517     3  0.0000      0.913 0.000 0.000 1.000  0
#&gt; ERR519484     1  0.1792      0.723 0.932 0.068 0.000  0
#&gt; ERR519498     1  0.1716      0.723 0.936 0.064 0.000  0
#&gt; ERR519490     3  0.4877      0.517 0.000 0.408 0.592  0
#&gt; ERR519507     1  0.4134      0.463 0.740 0.260 0.000  0
#&gt; ERR519511     1  0.4431      0.345 0.696 0.304 0.000  0
#&gt; ERR519468     1  0.4431      0.345 0.696 0.304 0.000  0
#&gt; ERR519482     2  0.4933      0.000 0.432 0.568 0.000  0
#&gt; ERR519475     1  0.0817      0.724 0.976 0.024 0.000  0
#&gt; ERR519496     1  0.4431      0.345 0.696 0.304 0.000  0
#&gt; ERR519506     1  0.1302      0.733 0.956 0.044 0.000  0
#&gt; ERR519469     1  0.4431      0.345 0.696 0.304 0.000  0
#&gt; ERR519480     4  0.0000      0.000 0.000 0.000 0.000  1
#&gt; ERR519487     3  0.0000      0.913 0.000 0.000 1.000  0
#&gt; ERR519483     1  0.0817      0.724 0.976 0.024 0.000  0
#&gt; ERR519477     1  0.0817      0.724 0.976 0.024 0.000  0
#&gt; ERR519499     3  0.0000      0.913 0.000 0.000 1.000  0
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-3-a').click(function(){
  $('#tab-CV-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-4'>
<p><a id='tab-CV-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3    p4 p5
#&gt; ERR519515     1  0.0290     0.8414 0.992 NA 0.000 0.008  0
#&gt; ERR519516     1  0.0703     0.8382 0.976 NA 0.000 0.024  0
#&gt; ERR519520     1  0.0290     0.8414 0.992 NA 0.000 0.008  0
#&gt; ERR519513     1  0.1571     0.8424 0.936 NA 0.000 0.060  0
#&gt; ERR519481     1  0.3003     0.8098 0.812 NA 0.000 0.188  0
#&gt; ERR519491     1  0.0609     0.8368 0.980 NA 0.000 0.020  0
#&gt; ERR519473     1  0.3816     0.7271 0.696 NA 0.000 0.304  0
#&gt; ERR519518     1  0.4273     0.5304 0.552 NA 0.000 0.448  0
#&gt; ERR519512     1  0.0290     0.8414 0.992 NA 0.000 0.008  0
#&gt; ERR519521     1  0.3003     0.8098 0.812 NA 0.000 0.188  0
#&gt; ERR519488     1  0.0290     0.8414 0.992 NA 0.000 0.008  0
#&gt; ERR519493     1  0.0609     0.8368 0.980 NA 0.000 0.020  0
#&gt; ERR519514     1  0.0290     0.8414 0.992 NA 0.000 0.008  0
#&gt; ERR519479     1  0.3003     0.8098 0.812 NA 0.000 0.188  0
#&gt; ERR519509     1  0.0290     0.8414 0.992 NA 0.000 0.008  0
#&gt; ERR519472     1  0.3730     0.7510 0.712 NA 0.000 0.288  0
#&gt; ERR519510     1  0.1671     0.8413 0.924 NA 0.000 0.076  0
#&gt; ERR519470     1  0.0290     0.8414 0.992 NA 0.000 0.008  0
#&gt; ERR519495     1  0.3816     0.7271 0.696 NA 0.000 0.304  0
#&gt; ERR519522     1  0.0290     0.8414 0.992 NA 0.000 0.008  0
#&gt; ERR519523     1  0.0290     0.8414 0.992 NA 0.000 0.008  0
#&gt; ERR519503     1  0.4273     0.5304 0.552 NA 0.000 0.448  0
#&gt; ERR519471     1  0.0290     0.8414 0.992 NA 0.000 0.008  0
#&gt; ERR519500     1  0.3424     0.7832 0.760 NA 0.000 0.240  0
#&gt; ERR519485     1  0.3816     0.7271 0.696 NA 0.000 0.304  0
#&gt; ERR519476     1  0.1725     0.8168 0.936 NA 0.000 0.020  0
#&gt; ERR519502     1  0.3109     0.8044 0.800 NA 0.000 0.200  0
#&gt; ERR519486     1  0.3816     0.7271 0.696 NA 0.000 0.304  0
#&gt; ERR519478     1  0.2605     0.7391 0.852 NA 0.000 0.148  0
#&gt; ERR519497     1  0.4273     0.5304 0.552 NA 0.000 0.448  0
#&gt; ERR519467     1  0.1725     0.8168 0.936 NA 0.000 0.020  0
#&gt; ERR519489     3  0.0000     0.4216 0.000 NA 1.000 0.000  0
#&gt; ERR519494     3  0.4291     0.7398 0.000 NA 0.536 0.000  0
#&gt; ERR519474     1  0.0703     0.8382 0.976 NA 0.000 0.024  0
#&gt; ERR519505     1  0.1117     0.8315 0.964 NA 0.000 0.020  0
#&gt; ERR519517     3  0.4291     0.7398 0.000 NA 0.536 0.000  0
#&gt; ERR519484     1  0.1732     0.8408 0.920 NA 0.000 0.080  0
#&gt; ERR519498     1  0.1571     0.8424 0.936 NA 0.000 0.060  0
#&gt; ERR519490     3  0.4088    -0.0512 0.000 NA 0.632 0.000  0
#&gt; ERR519507     1  0.3636     0.7627 0.728 NA 0.000 0.272  0
#&gt; ERR519511     1  0.3816     0.7271 0.696 NA 0.000 0.304  0
#&gt; ERR519468     1  0.3816     0.7271 0.696 NA 0.000 0.304  0
#&gt; ERR519482     4  0.1608     0.0000 0.000 NA 0.000 0.928  0
#&gt; ERR519475     1  0.1725     0.8168 0.936 NA 0.000 0.020  0
#&gt; ERR519496     1  0.4273     0.5304 0.552 NA 0.000 0.448  0
#&gt; ERR519506     1  0.1121     0.8449 0.956 NA 0.000 0.044  0
#&gt; ERR519469     1  0.3816     0.7271 0.696 NA 0.000 0.304  0
#&gt; ERR519480     5  0.0000     0.0000 0.000 NA 0.000 0.000  1
#&gt; ERR519487     3  0.4291     0.7398 0.000 NA 0.536 0.000  0
#&gt; ERR519483     1  0.2561     0.8045 0.884 NA 0.000 0.020  0
#&gt; ERR519477     1  0.1725     0.8168 0.936 NA 0.000 0.020  0
#&gt; ERR519499     3  0.4291     0.7398 0.000 NA 0.536 0.000  0
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-4-a').click(function(){
  $('#tab-CV-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-5'>
<p><a id='tab-CV-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3    p4    p5    p6
#&gt; ERR519515     1  0.0146      0.786 0.996  0 0.000 0.000 0.004 0.000
#&gt; ERR519516     1  0.0713      0.780 0.972  0 0.000 0.000 0.028 0.000
#&gt; ERR519520     1  0.0146      0.786 0.996  0 0.000 0.000 0.004 0.000
#&gt; ERR519513     1  0.1387      0.791 0.932  0 0.000 0.000 0.068 0.000
#&gt; ERR519481     1  0.3426      0.757 0.808  0 0.000 0.000 0.124 0.068
#&gt; ERR519491     1  0.0632      0.778 0.976  0 0.000 0.000 0.024 0.000
#&gt; ERR519473     1  0.4566      0.674 0.700  0 0.000 0.000 0.160 0.140
#&gt; ERR519518     1  0.5453      0.464 0.556  0 0.000 0.000 0.160 0.284
#&gt; ERR519512     1  0.0146      0.786 0.996  0 0.000 0.000 0.004 0.000
#&gt; ERR519521     1  0.3426      0.757 0.808  0 0.000 0.000 0.124 0.068
#&gt; ERR519488     1  0.0146      0.786 0.996  0 0.000 0.000 0.004 0.000
#&gt; ERR519493     1  0.0632      0.778 0.976  0 0.000 0.000 0.024 0.000
#&gt; ERR519514     1  0.0146      0.786 0.996  0 0.000 0.000 0.004 0.000
#&gt; ERR519479     1  0.3426      0.757 0.808  0 0.000 0.000 0.124 0.068
#&gt; ERR519509     1  0.0146      0.786 0.996  0 0.000 0.000 0.004 0.000
#&gt; ERR519472     1  0.4466      0.696 0.708  0 0.000 0.000 0.176 0.116
#&gt; ERR519510     1  0.1556      0.789 0.920  0 0.000 0.000 0.080 0.000
#&gt; ERR519470     1  0.0146      0.786 0.996  0 0.000 0.000 0.004 0.000
#&gt; ERR519495     1  0.4566      0.674 0.700  0 0.000 0.000 0.160 0.140
#&gt; ERR519522     1  0.0146      0.786 0.996  0 0.000 0.000 0.004 0.000
#&gt; ERR519523     1  0.0146      0.786 0.996  0 0.000 0.000 0.004 0.000
#&gt; ERR519503     1  0.5453      0.464 0.556  0 0.000 0.000 0.160 0.284
#&gt; ERR519471     1  0.0146      0.786 0.996  0 0.000 0.000 0.004 0.000
#&gt; ERR519500     1  0.4003      0.730 0.756  0 0.000 0.000 0.152 0.092
#&gt; ERR519485     1  0.4566      0.674 0.700  0 0.000 0.000 0.160 0.140
#&gt; ERR519476     1  0.1616      0.744 0.932  0 0.000 0.020 0.048 0.000
#&gt; ERR519502     1  0.3563      0.752 0.796  0 0.000 0.000 0.132 0.072
#&gt; ERR519486     1  0.4566      0.674 0.700  0 0.000 0.000 0.160 0.140
#&gt; ERR519478     1  0.2402      0.639 0.856  0 0.000 0.000 0.004 0.140
#&gt; ERR519497     1  0.5453      0.464 0.556  0 0.000 0.000 0.160 0.284
#&gt; ERR519467     1  0.1616      0.744 0.932  0 0.000 0.020 0.048 0.000
#&gt; ERR519489     4  0.5587      0.566 0.000  0 0.272 0.540 0.188 0.000
#&gt; ERR519494     3  0.0000      1.000 0.000  0 1.000 0.000 0.000 0.000
#&gt; ERR519474     1  0.0713      0.780 0.972  0 0.000 0.000 0.028 0.000
#&gt; ERR519505     1  0.1049      0.769 0.960  0 0.000 0.008 0.032 0.000
#&gt; ERR519517     3  0.0000      1.000 0.000  0 1.000 0.000 0.000 0.000
#&gt; ERR519484     1  0.1610      0.788 0.916  0 0.000 0.000 0.084 0.000
#&gt; ERR519498     1  0.1387      0.791 0.932  0 0.000 0.000 0.068 0.000
#&gt; ERR519490     4  0.1267      0.541 0.000  0 0.060 0.940 0.000 0.000
#&gt; ERR519507     1  0.4319      0.708 0.724  0 0.000 0.000 0.168 0.108
#&gt; ERR519511     1  0.4566      0.674 0.700  0 0.000 0.000 0.160 0.140
#&gt; ERR519468     1  0.4566      0.674 0.700  0 0.000 0.000 0.160 0.140
#&gt; ERR519482     6  0.0000      0.000 0.000  0 0.000 0.000 0.000 1.000
#&gt; ERR519475     1  0.1616      0.744 0.932  0 0.000 0.020 0.048 0.000
#&gt; ERR519496     1  0.5453      0.464 0.556  0 0.000 0.000 0.160 0.284
#&gt; ERR519506     1  0.0937      0.793 0.960  0 0.000 0.000 0.040 0.000
#&gt; ERR519469     1  0.4566      0.674 0.700  0 0.000 0.000 0.160 0.140
#&gt; ERR519480     2  0.0000      0.000 0.000  1 0.000 0.000 0.000 0.000
#&gt; ERR519487     3  0.0000      1.000 0.000  0 1.000 0.000 0.000 0.000
#&gt; ERR519483     5  0.4348      0.000 0.320  0 0.000 0.040 0.640 0.000
#&gt; ERR519477     1  0.1616      0.744 0.932  0 0.000 0.020 0.048 0.000
#&gt; ERR519499     3  0.0000      1.000 0.000  0 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-5-a').click(function(){
  $('#tab-CV-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-CV-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-get-signatures'>
<ul>
<li><a href='#tab-CV-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-1-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-1"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-2-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-2"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-3-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-3"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-4-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-4"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-5-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-hclust-signature_compare](figure_cola/CV-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-CV-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-hclust-collect-classes](figure_cola/CV-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:kmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "kmeans"]
# you can also extract it by
# res = res_list["CV:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 18140 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-kmeans-collect-plots](figure_cola/CV-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-kmeans-select-partition-number](figure_cola/CV-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.2383 0.762   0.762
#> 3 3 0.448           0.681       0.803         1.1225 0.736   0.654
#> 4 4 0.470           0.638       0.817         0.1765 0.795   0.628
#> 5 5 0.476           0.471       0.714         0.1447 0.905   0.766
#> 6 6 0.477           0.581       0.755         0.0919 0.856   0.584
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-get-classes'>
<ul>
<li><a href='#tab-CV-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-kmeans-get-classes-1'>
<p><a id='tab-CV-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette p1 p2
#&gt; ERR519515     1       0          1  1  0
#&gt; ERR519516     1       0          1  1  0
#&gt; ERR519520     1       0          1  1  0
#&gt; ERR519513     1       0          1  1  0
#&gt; ERR519481     1       0          1  1  0
#&gt; ERR519491     1       0          1  1  0
#&gt; ERR519473     1       0          1  1  0
#&gt; ERR519518     1       0          1  1  0
#&gt; ERR519512     1       0          1  1  0
#&gt; ERR519521     1       0          1  1  0
#&gt; ERR519488     1       0          1  1  0
#&gt; ERR519493     1       0          1  1  0
#&gt; ERR519514     1       0          1  1  0
#&gt; ERR519479     1       0          1  1  0
#&gt; ERR519509     1       0          1  1  0
#&gt; ERR519472     1       0          1  1  0
#&gt; ERR519510     1       0          1  1  0
#&gt; ERR519470     1       0          1  1  0
#&gt; ERR519495     1       0          1  1  0
#&gt; ERR519522     1       0          1  1  0
#&gt; ERR519523     1       0          1  1  0
#&gt; ERR519503     1       0          1  1  0
#&gt; ERR519471     1       0          1  1  0
#&gt; ERR519500     1       0          1  1  0
#&gt; ERR519485     1       0          1  1  0
#&gt; ERR519476     1       0          1  1  0
#&gt; ERR519502     1       0          1  1  0
#&gt; ERR519486     1       0          1  1  0
#&gt; ERR519478     1       0          1  1  0
#&gt; ERR519497     1       0          1  1  0
#&gt; ERR519467     1       0          1  1  0
#&gt; ERR519489     2       0          1  0  1
#&gt; ERR519494     2       0          1  0  1
#&gt; ERR519474     1       0          1  1  0
#&gt; ERR519505     1       0          1  1  0
#&gt; ERR519517     2       0          1  0  1
#&gt; ERR519484     1       0          1  1  0
#&gt; ERR519498     1       0          1  1  0
#&gt; ERR519490     2       0          1  0  1
#&gt; ERR519507     1       0          1  1  0
#&gt; ERR519511     1       0          1  1  0
#&gt; ERR519468     1       0          1  1  0
#&gt; ERR519482     1       0          1  1  0
#&gt; ERR519475     1       0          1  1  0
#&gt; ERR519496     1       0          1  1  0
#&gt; ERR519506     1       0          1  1  0
#&gt; ERR519469     1       0          1  1  0
#&gt; ERR519480     2       0          1  0  1
#&gt; ERR519487     2       0          1  0  1
#&gt; ERR519483     1       0          1  1  0
#&gt; ERR519477     1       0          1  1  0
#&gt; ERR519499     2       0          1  0  1
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-1-a').click(function(){
  $('#tab-CV-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-2'>
<p><a id='tab-CV-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; ERR519515     1  0.0000     0.7696 1.000 0.000 0.000
#&gt; ERR519516     1  0.0000     0.7696 1.000 0.000 0.000
#&gt; ERR519520     1  0.5706     0.4991 0.680 0.320 0.000
#&gt; ERR519513     1  0.6154     0.2334 0.592 0.408 0.000
#&gt; ERR519481     1  0.5785     0.4428 0.668 0.332 0.000
#&gt; ERR519491     1  0.0000     0.7696 1.000 0.000 0.000
#&gt; ERR519473     2  0.6095     0.5725 0.392 0.608 0.000
#&gt; ERR519518     2  0.4062     0.8753 0.164 0.836 0.000
#&gt; ERR519512     1  0.5178     0.5661 0.744 0.256 0.000
#&gt; ERR519521     1  0.5678     0.4803 0.684 0.316 0.000
#&gt; ERR519488     1  0.0237     0.7683 0.996 0.004 0.000
#&gt; ERR519493     1  0.0000     0.7696 1.000 0.000 0.000
#&gt; ERR519514     1  0.0000     0.7696 1.000 0.000 0.000
#&gt; ERR519479     1  0.4291     0.6587 0.820 0.180 0.000
#&gt; ERR519509     1  0.2066     0.7306 0.940 0.060 0.000
#&gt; ERR519472     1  0.6095     0.2867 0.608 0.392 0.000
#&gt; ERR519510     1  0.2165     0.7467 0.936 0.064 0.000
#&gt; ERR519470     1  0.0000     0.7696 1.000 0.000 0.000
#&gt; ERR519495     2  0.5497     0.8229 0.292 0.708 0.000
#&gt; ERR519522     1  0.0237     0.7683 0.996 0.004 0.000
#&gt; ERR519523     1  0.3482     0.7016 0.872 0.128 0.000
#&gt; ERR519503     2  0.4235     0.8840 0.176 0.824 0.000
#&gt; ERR519471     1  0.0000     0.7696 1.000 0.000 0.000
#&gt; ERR519500     1  0.6079     0.3000 0.612 0.388 0.000
#&gt; ERR519485     1  0.4002     0.6572 0.840 0.160 0.000
#&gt; ERR519476     1  0.2066     0.7264 0.940 0.060 0.000
#&gt; ERR519502     1  0.6045     0.3265 0.620 0.380 0.000
#&gt; ERR519486     2  0.5363     0.8437 0.276 0.724 0.000
#&gt; ERR519478     1  0.2625     0.7073 0.916 0.084 0.000
#&gt; ERR519497     2  0.4291     0.8865 0.180 0.820 0.000
#&gt; ERR519467     1  0.0237     0.7683 0.996 0.004 0.000
#&gt; ERR519489     3  0.0000     0.9553 0.000 0.000 1.000
#&gt; ERR519494     3  0.0000     0.9553 0.000 0.000 1.000
#&gt; ERR519474     1  0.0000     0.7696 1.000 0.000 0.000
#&gt; ERR519505     1  0.0237     0.7693 0.996 0.004 0.000
#&gt; ERR519517     3  0.0000     0.9553 0.000 0.000 1.000
#&gt; ERR519484     1  0.0424     0.7686 0.992 0.008 0.000
#&gt; ERR519498     1  0.5706     0.4673 0.680 0.320 0.000
#&gt; ERR519490     3  0.0000     0.9553 0.000 0.000 1.000
#&gt; ERR519507     1  0.6045     0.3245 0.620 0.380 0.000
#&gt; ERR519511     2  0.4750     0.8812 0.216 0.784 0.000
#&gt; ERR519468     2  0.5363     0.8387 0.276 0.724 0.000
#&gt; ERR519482     2  0.4062     0.8753 0.164 0.836 0.000
#&gt; ERR519475     1  0.2066     0.7264 0.940 0.060 0.000
#&gt; ERR519496     2  0.4291     0.8865 0.180 0.820 0.000
#&gt; ERR519506     1  0.0237     0.7693 0.996 0.004 0.000
#&gt; ERR519469     1  0.6299    -0.0753 0.524 0.476 0.000
#&gt; ERR519480     3  0.5926     0.6647 0.000 0.356 0.644
#&gt; ERR519487     3  0.0000     0.9553 0.000 0.000 1.000
#&gt; ERR519483     1  0.6309    -0.3754 0.504 0.496 0.000
#&gt; ERR519477     1  0.2066     0.7264 0.940 0.060 0.000
#&gt; ERR519499     3  0.0000     0.9553 0.000 0.000 1.000
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-2-a').click(function(){
  $('#tab-CV-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-3'>
<p><a id='tab-CV-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; ERR519515     1  0.1256     0.8150 0.964 0.028 0.000 0.008
#&gt; ERR519516     1  0.0524     0.8148 0.988 0.008 0.000 0.004
#&gt; ERR519520     1  0.5916     0.4927 0.656 0.072 0.000 0.272
#&gt; ERR519513     4  0.5775     0.3935 0.408 0.032 0.000 0.560
#&gt; ERR519481     1  0.5558    -0.0139 0.548 0.020 0.000 0.432
#&gt; ERR519491     1  0.0000     0.8158 1.000 0.000 0.000 0.000
#&gt; ERR519473     4  0.2469     0.6397 0.108 0.000 0.000 0.892
#&gt; ERR519518     4  0.3161     0.5435 0.012 0.124 0.000 0.864
#&gt; ERR519512     1  0.5489     0.5278 0.700 0.060 0.000 0.240
#&gt; ERR519521     1  0.5476     0.1533 0.584 0.020 0.000 0.396
#&gt; ERR519488     1  0.2342     0.8050 0.912 0.080 0.000 0.008
#&gt; ERR519493     1  0.0779     0.8136 0.980 0.016 0.000 0.004
#&gt; ERR519514     1  0.1151     0.8154 0.968 0.024 0.000 0.008
#&gt; ERR519479     1  0.3681     0.6643 0.816 0.008 0.000 0.176
#&gt; ERR519509     1  0.3439     0.7767 0.868 0.084 0.000 0.048
#&gt; ERR519472     4  0.4998     0.2213 0.488 0.000 0.000 0.512
#&gt; ERR519510     1  0.3216     0.7696 0.880 0.044 0.000 0.076
#&gt; ERR519470     1  0.1256     0.8150 0.964 0.028 0.000 0.008
#&gt; ERR519495     4  0.2401     0.6357 0.092 0.004 0.000 0.904
#&gt; ERR519522     1  0.2198     0.8068 0.920 0.072 0.000 0.008
#&gt; ERR519523     1  0.3554     0.7222 0.844 0.020 0.000 0.136
#&gt; ERR519503     4  0.5200     0.5010 0.072 0.184 0.000 0.744
#&gt; ERR519471     1  0.1151     0.8154 0.968 0.024 0.000 0.008
#&gt; ERR519500     4  0.4998     0.2213 0.488 0.000 0.000 0.512
#&gt; ERR519485     1  0.4720     0.3562 0.672 0.004 0.000 0.324
#&gt; ERR519476     1  0.3356     0.7260 0.824 0.176 0.000 0.000
#&gt; ERR519502     4  0.5607     0.1978 0.488 0.020 0.000 0.492
#&gt; ERR519486     4  0.2412     0.6317 0.084 0.008 0.000 0.908
#&gt; ERR519478     1  0.3745     0.7631 0.852 0.088 0.000 0.060
#&gt; ERR519497     4  0.3948     0.5628 0.036 0.136 0.000 0.828
#&gt; ERR519467     1  0.1867     0.8089 0.928 0.072 0.000 0.000
#&gt; ERR519489     3  0.0336     0.9926 0.000 0.000 0.992 0.008
#&gt; ERR519494     3  0.0000     0.9963 0.000 0.000 1.000 0.000
#&gt; ERR519474     1  0.0592     0.8146 0.984 0.016 0.000 0.000
#&gt; ERR519505     1  0.1489     0.8109 0.952 0.044 0.000 0.004
#&gt; ERR519517     3  0.0000     0.9963 0.000 0.000 1.000 0.000
#&gt; ERR519484     1  0.1356     0.8103 0.960 0.032 0.000 0.008
#&gt; ERR519498     1  0.5755     0.2987 0.624 0.044 0.000 0.332
#&gt; ERR519490     3  0.0336     0.9926 0.000 0.000 0.992 0.008
#&gt; ERR519507     4  0.5165     0.2231 0.484 0.004 0.000 0.512
#&gt; ERR519511     4  0.1635     0.6013 0.044 0.008 0.000 0.948
#&gt; ERR519468     4  0.2197     0.6281 0.080 0.004 0.000 0.916
#&gt; ERR519482     4  0.3047     0.5425 0.012 0.116 0.000 0.872
#&gt; ERR519475     1  0.3356     0.7260 0.824 0.176 0.000 0.000
#&gt; ERR519496     4  0.4673     0.5506 0.076 0.132 0.000 0.792
#&gt; ERR519506     1  0.1151     0.8163 0.968 0.024 0.000 0.008
#&gt; ERR519469     4  0.3975     0.6213 0.240 0.000 0.000 0.760
#&gt; ERR519480     2  0.6397     0.0000 0.000 0.648 0.208 0.144
#&gt; ERR519487     3  0.0000     0.9963 0.000 0.000 1.000 0.000
#&gt; ERR519483     4  0.5482     0.4380 0.368 0.024 0.000 0.608
#&gt; ERR519477     1  0.3356     0.7260 0.824 0.176 0.000 0.000
#&gt; ERR519499     3  0.0000     0.9963 0.000 0.000 1.000 0.000
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-3-a').click(function(){
  $('#tab-CV-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-4'>
<p><a id='tab-CV-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; ERR519515     1  0.0162      0.719 0.996 0.000 0.000 0.000 0.004
#&gt; ERR519516     1  0.2732      0.681 0.840 0.000 0.000 0.000 0.160
#&gt; ERR519520     1  0.6231      0.426 0.604 0.056 0.000 0.068 0.272
#&gt; ERR519513     5  0.6736      0.326 0.168 0.028 0.000 0.264 0.540
#&gt; ERR519481     5  0.7304      0.462 0.292 0.024 0.000 0.292 0.392
#&gt; ERR519491     1  0.1270      0.720 0.948 0.000 0.000 0.000 0.052
#&gt; ERR519473     4  0.4787      0.414 0.012 0.004 0.000 0.528 0.456
#&gt; ERR519518     4  0.1282      0.400 0.000 0.004 0.000 0.952 0.044
#&gt; ERR519512     1  0.6592      0.301 0.560 0.044 0.000 0.108 0.288
#&gt; ERR519521     1  0.7619     -0.333 0.380 0.048 0.000 0.256 0.316
#&gt; ERR519488     1  0.3049      0.679 0.876 0.048 0.000 0.012 0.064
#&gt; ERR519493     1  0.2605      0.690 0.852 0.000 0.000 0.000 0.148
#&gt; ERR519514     1  0.0794      0.721 0.972 0.000 0.000 0.000 0.028
#&gt; ERR519479     1  0.4801      0.450 0.668 0.000 0.000 0.048 0.284
#&gt; ERR519509     1  0.3152      0.676 0.872 0.048 0.000 0.016 0.064
#&gt; ERR519472     4  0.6764     -0.307 0.308 0.000 0.000 0.400 0.292
#&gt; ERR519510     1  0.5834     -0.010 0.500 0.032 0.000 0.036 0.432
#&gt; ERR519470     1  0.0162      0.719 0.996 0.000 0.000 0.000 0.004
#&gt; ERR519495     4  0.4877      0.432 0.016 0.004 0.000 0.524 0.456
#&gt; ERR519522     1  0.2519      0.688 0.900 0.036 0.000 0.004 0.060
#&gt; ERR519523     1  0.3012      0.668 0.852 0.000 0.000 0.024 0.124
#&gt; ERR519503     4  0.4911      0.251 0.144 0.012 0.000 0.740 0.104
#&gt; ERR519471     1  0.0794      0.721 0.972 0.000 0.000 0.000 0.028
#&gt; ERR519500     4  0.6783     -0.335 0.316 0.000 0.000 0.388 0.296
#&gt; ERR519485     5  0.6167      0.149 0.348 0.004 0.000 0.128 0.520
#&gt; ERR519476     1  0.4369      0.568 0.740 0.052 0.000 0.000 0.208
#&gt; ERR519502     5  0.7341      0.452 0.268 0.028 0.000 0.304 0.400
#&gt; ERR519486     4  0.4877      0.432 0.016 0.004 0.000 0.524 0.456
#&gt; ERR519478     1  0.3427      0.667 0.860 0.048 0.000 0.028 0.064
#&gt; ERR519497     4  0.3561      0.340 0.008 0.008 0.000 0.796 0.188
#&gt; ERR519467     1  0.2149      0.700 0.916 0.036 0.000 0.000 0.048
#&gt; ERR519489     3  0.0703      0.980 0.000 0.000 0.976 0.000 0.024
#&gt; ERR519494     3  0.0000      0.990 0.000 0.000 1.000 0.000 0.000
#&gt; ERR519474     1  0.1671      0.715 0.924 0.000 0.000 0.000 0.076
#&gt; ERR519505     1  0.5121      0.506 0.648 0.040 0.000 0.012 0.300
#&gt; ERR519517     3  0.0000      0.990 0.000 0.000 1.000 0.000 0.000
#&gt; ERR519484     1  0.5096      0.417 0.636 0.024 0.000 0.020 0.320
#&gt; ERR519498     5  0.6805      0.251 0.400 0.028 0.000 0.132 0.440
#&gt; ERR519490     3  0.0703      0.980 0.000 0.000 0.976 0.000 0.024
#&gt; ERR519507     4  0.6813     -0.347 0.316 0.000 0.000 0.364 0.320
#&gt; ERR519511     4  0.4698      0.432 0.008 0.004 0.000 0.520 0.468
#&gt; ERR519468     4  0.4686      0.437 0.012 0.004 0.000 0.588 0.396
#&gt; ERR519482     4  0.0865      0.404 0.000 0.004 0.000 0.972 0.024
#&gt; ERR519475     1  0.4369      0.568 0.740 0.052 0.000 0.000 0.208
#&gt; ERR519496     4  0.4403      0.307 0.132 0.004 0.000 0.772 0.092
#&gt; ERR519506     1  0.2179      0.710 0.888 0.000 0.000 0.000 0.112
#&gt; ERR519469     4  0.4969      0.384 0.020 0.004 0.000 0.508 0.468
#&gt; ERR519480     2  0.2850      0.000 0.000 0.872 0.092 0.036 0.000
#&gt; ERR519487     3  0.0000      0.990 0.000 0.000 1.000 0.000 0.000
#&gt; ERR519483     5  0.6459     -0.234 0.180 0.004 0.000 0.312 0.504
#&gt; ERR519477     1  0.4369      0.568 0.740 0.052 0.000 0.000 0.208
#&gt; ERR519499     3  0.0000      0.990 0.000 0.000 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-4-a').click(function(){
  $('#tab-CV-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-5'>
<p><a id='tab-CV-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; ERR519515     1  0.0520     0.7436 0.984 0.000 0.000 0.008 0.008 0.000
#&gt; ERR519516     1  0.4139     0.3630 0.644 0.008 0.000 0.336 0.012 0.000
#&gt; ERR519520     1  0.6339    -0.0047 0.472 0.080 0.000 0.384 0.048 0.016
#&gt; ERR519513     4  0.4031     0.6698 0.060 0.004 0.000 0.748 0.188 0.000
#&gt; ERR519481     4  0.5307     0.7319 0.128 0.024 0.000 0.652 0.196 0.000
#&gt; ERR519491     1  0.1983     0.7294 0.916 0.012 0.000 0.060 0.012 0.000
#&gt; ERR519473     5  0.2696     0.4713 0.004 0.048 0.000 0.076 0.872 0.000
#&gt; ERR519518     2  0.4977     0.6366 0.000 0.552 0.000 0.076 0.372 0.000
#&gt; ERR519512     4  0.5754     0.2692 0.384 0.020 0.000 0.512 0.072 0.012
#&gt; ERR519521     4  0.5141     0.7410 0.132 0.024 0.000 0.676 0.168 0.000
#&gt; ERR519488     1  0.3405     0.6858 0.832 0.068 0.000 0.084 0.000 0.016
#&gt; ERR519493     1  0.4086     0.4411 0.676 0.012 0.000 0.300 0.012 0.000
#&gt; ERR519514     1  0.0717     0.7433 0.976 0.000 0.000 0.008 0.016 0.000
#&gt; ERR519479     1  0.5477    -0.2115 0.476 0.008 0.000 0.420 0.096 0.000
#&gt; ERR519509     1  0.3460     0.6830 0.828 0.072 0.000 0.084 0.000 0.016
#&gt; ERR519472     5  0.6205     0.1546 0.296 0.020 0.000 0.200 0.484 0.000
#&gt; ERR519510     4  0.3752     0.7829 0.164 0.000 0.000 0.772 0.064 0.000
#&gt; ERR519470     1  0.0520     0.7436 0.984 0.000 0.000 0.008 0.008 0.000
#&gt; ERR519495     5  0.1410     0.4832 0.008 0.004 0.000 0.044 0.944 0.000
#&gt; ERR519522     1  0.2649     0.7130 0.884 0.052 0.000 0.048 0.000 0.016
#&gt; ERR519523     1  0.3368     0.6624 0.828 0.012 0.000 0.108 0.052 0.000
#&gt; ERR519503     2  0.6174     0.5773 0.180 0.528 0.000 0.032 0.260 0.000
#&gt; ERR519471     1  0.0717     0.7433 0.976 0.000 0.000 0.008 0.016 0.000
#&gt; ERR519500     5  0.6243     0.1347 0.296 0.020 0.000 0.208 0.476 0.000
#&gt; ERR519485     5  0.4905     0.3168 0.264 0.004 0.000 0.092 0.640 0.000
#&gt; ERR519476     1  0.4313     0.5678 0.668 0.284 0.000 0.048 0.000 0.000
#&gt; ERR519502     4  0.5260     0.7266 0.120 0.024 0.000 0.656 0.200 0.000
#&gt; ERR519486     5  0.1781     0.4761 0.008 0.008 0.000 0.060 0.924 0.000
#&gt; ERR519478     1  0.3717     0.6674 0.808 0.092 0.000 0.084 0.000 0.016
#&gt; ERR519497     2  0.5956     0.5640 0.004 0.472 0.000 0.208 0.316 0.000
#&gt; ERR519467     1  0.2084     0.7247 0.916 0.024 0.000 0.044 0.000 0.016
#&gt; ERR519489     3  0.1633     0.9508 0.000 0.024 0.932 0.044 0.000 0.000
#&gt; ERR519494     3  0.0000     0.9733 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519474     1  0.2159     0.7239 0.904 0.012 0.000 0.072 0.012 0.000
#&gt; ERR519505     4  0.3109     0.7249 0.224 0.004 0.000 0.772 0.000 0.000
#&gt; ERR519517     3  0.0000     0.9733 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519484     4  0.4055     0.7439 0.228 0.008 0.000 0.728 0.036 0.000
#&gt; ERR519498     4  0.3946     0.7834 0.152 0.004 0.000 0.768 0.076 0.000
#&gt; ERR519490     3  0.1716     0.9498 0.000 0.028 0.932 0.036 0.004 0.000
#&gt; ERR519507     5  0.5881     0.1083 0.296 0.000 0.000 0.232 0.472 0.000
#&gt; ERR519511     5  0.2001     0.4689 0.008 0.012 0.000 0.068 0.912 0.000
#&gt; ERR519468     5  0.3079     0.3800 0.004 0.096 0.000 0.056 0.844 0.000
#&gt; ERR519482     2  0.4534     0.6209 0.000 0.580 0.000 0.040 0.380 0.000
#&gt; ERR519475     1  0.4313     0.5678 0.668 0.284 0.000 0.048 0.000 0.000
#&gt; ERR519496     2  0.6043     0.5747 0.124 0.464 0.000 0.028 0.384 0.000
#&gt; ERR519506     1  0.3504     0.6882 0.820 0.016 0.000 0.112 0.052 0.000
#&gt; ERR519469     5  0.2808     0.4745 0.008 0.048 0.000 0.076 0.868 0.000
#&gt; ERR519480     6  0.0458     0.0000 0.000 0.000 0.016 0.000 0.000 0.984
#&gt; ERR519487     3  0.0363     0.9717 0.000 0.000 0.988 0.012 0.000 0.000
#&gt; ERR519483     5  0.5419     0.2757 0.112 0.060 0.000 0.156 0.672 0.000
#&gt; ERR519477     1  0.4313     0.5678 0.668 0.284 0.000 0.048 0.000 0.000
#&gt; ERR519499     3  0.0000     0.9733 0.000 0.000 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-5-a').click(function(){
  $('#tab-CV-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-CV-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-get-signatures'>
<ul>
<li><a href='#tab-CV-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-kmeans-signature_compare](figure_cola/CV-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-CV-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-kmeans-collect-classes](figure_cola/CV-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:skmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "skmeans"]
# you can also extract it by
# res = res_list["CV:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 18140 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-skmeans-collect-plots](figure_cola/CV-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-skmeans-select-partition-number](figure_cola/CV-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.960           0.936       0.975          0.406 0.599   0.599
#> 3 3 0.590           0.627       0.776          0.454 0.673   0.489
#> 4 4 0.539           0.522       0.759          0.152 0.722   0.425
#> 5 5 0.667           0.685       0.829          0.112 0.827   0.553
#> 6 6 0.715           0.696       0.794          0.053 0.926   0.727
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-get-classes'>
<ul>
<li><a href='#tab-CV-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-skmeans-get-classes-1'>
<p><a id='tab-CV-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; ERR519515     1   0.000     0.9779 1.000 0.000
#&gt; ERR519516     1   0.000     0.9779 1.000 0.000
#&gt; ERR519520     1   0.000     0.9779 1.000 0.000
#&gt; ERR519513     1   0.000     0.9779 1.000 0.000
#&gt; ERR519481     1   0.000     0.9779 1.000 0.000
#&gt; ERR519491     1   0.000     0.9779 1.000 0.000
#&gt; ERR519473     1   1.000    -0.0708 0.504 0.496
#&gt; ERR519518     2   0.000     0.9580 0.000 1.000
#&gt; ERR519512     1   0.000     0.9779 1.000 0.000
#&gt; ERR519521     1   0.000     0.9779 1.000 0.000
#&gt; ERR519488     1   0.000     0.9779 1.000 0.000
#&gt; ERR519493     1   0.000     0.9779 1.000 0.000
#&gt; ERR519514     1   0.000     0.9779 1.000 0.000
#&gt; ERR519479     1   0.000     0.9779 1.000 0.000
#&gt; ERR519509     1   0.000     0.9779 1.000 0.000
#&gt; ERR519472     1   0.000     0.9779 1.000 0.000
#&gt; ERR519510     1   0.000     0.9779 1.000 0.000
#&gt; ERR519470     1   0.000     0.9779 1.000 0.000
#&gt; ERR519495     2   0.388     0.8997 0.076 0.924
#&gt; ERR519522     1   0.000     0.9779 1.000 0.000
#&gt; ERR519523     1   0.000     0.9779 1.000 0.000
#&gt; ERR519503     2   0.775     0.7076 0.228 0.772
#&gt; ERR519471     1   0.000     0.9779 1.000 0.000
#&gt; ERR519500     1   0.000     0.9779 1.000 0.000
#&gt; ERR519485     1   0.000     0.9779 1.000 0.000
#&gt; ERR519476     1   0.000     0.9779 1.000 0.000
#&gt; ERR519502     1   0.000     0.9779 1.000 0.000
#&gt; ERR519486     2   0.000     0.9580 0.000 1.000
#&gt; ERR519478     1   0.000     0.9779 1.000 0.000
#&gt; ERR519497     1   0.430     0.8867 0.912 0.088
#&gt; ERR519467     1   0.000     0.9779 1.000 0.000
#&gt; ERR519489     2   0.000     0.9580 0.000 1.000
#&gt; ERR519494     2   0.000     0.9580 0.000 1.000
#&gt; ERR519474     1   0.000     0.9779 1.000 0.000
#&gt; ERR519505     1   0.000     0.9779 1.000 0.000
#&gt; ERR519517     2   0.000     0.9580 0.000 1.000
#&gt; ERR519484     1   0.000     0.9779 1.000 0.000
#&gt; ERR519498     1   0.000     0.9779 1.000 0.000
#&gt; ERR519490     2   0.000     0.9580 0.000 1.000
#&gt; ERR519507     1   0.000     0.9779 1.000 0.000
#&gt; ERR519511     2   0.000     0.9580 0.000 1.000
#&gt; ERR519468     2   0.760     0.7307 0.220 0.780
#&gt; ERR519482     2   0.000     0.9580 0.000 1.000
#&gt; ERR519475     1   0.000     0.9779 1.000 0.000
#&gt; ERR519496     1   0.689     0.7618 0.816 0.184
#&gt; ERR519506     1   0.000     0.9779 1.000 0.000
#&gt; ERR519469     1   0.000     0.9779 1.000 0.000
#&gt; ERR519480     2   0.000     0.9580 0.000 1.000
#&gt; ERR519487     2   0.000     0.9580 0.000 1.000
#&gt; ERR519483     1   0.000     0.9779 1.000 0.000
#&gt; ERR519477     1   0.000     0.9779 1.000 0.000
#&gt; ERR519499     2   0.000     0.9580 0.000 1.000
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-1-a').click(function(){
  $('#tab-CV-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-2'>
<p><a id='tab-CV-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; ERR519515     1  0.6095      0.762 0.608 0.392 0.000
#&gt; ERR519516     1  0.6215      0.716 0.572 0.428 0.000
#&gt; ERR519520     1  0.2537      0.348 0.920 0.080 0.000
#&gt; ERR519513     2  0.2537      0.638 0.080 0.920 0.000
#&gt; ERR519481     2  0.1964      0.646 0.056 0.944 0.000
#&gt; ERR519491     1  0.6126      0.760 0.600 0.400 0.000
#&gt; ERR519473     2  0.0661      0.636 0.004 0.988 0.008
#&gt; ERR519518     2  0.6632      0.309 0.392 0.596 0.012
#&gt; ERR519512     2  0.3879      0.603 0.152 0.848 0.000
#&gt; ERR519521     2  0.5216      0.529 0.260 0.740 0.000
#&gt; ERR519488     1  0.3412      0.498 0.876 0.124 0.000
#&gt; ERR519493     1  0.6192      0.730 0.580 0.420 0.000
#&gt; ERR519514     1  0.6095      0.762 0.608 0.392 0.000
#&gt; ERR519479     1  0.6309      0.555 0.504 0.496 0.000
#&gt; ERR519509     1  0.1031      0.413 0.976 0.024 0.000
#&gt; ERR519472     2  0.3038      0.625 0.104 0.896 0.000
#&gt; ERR519510     2  0.6140     -0.283 0.404 0.596 0.000
#&gt; ERR519470     1  0.6095      0.762 0.608 0.392 0.000
#&gt; ERR519495     3  0.1643      0.945 0.000 0.044 0.956
#&gt; ERR519522     1  0.6062      0.757 0.616 0.384 0.000
#&gt; ERR519523     1  0.6111      0.761 0.604 0.396 0.000
#&gt; ERR519503     1  0.3998      0.255 0.884 0.056 0.060
#&gt; ERR519471     1  0.6095      0.762 0.608 0.392 0.000
#&gt; ERR519500     2  0.3267      0.616 0.116 0.884 0.000
#&gt; ERR519485     1  0.6111      0.761 0.604 0.396 0.000
#&gt; ERR519476     1  0.6126      0.760 0.600 0.400 0.000
#&gt; ERR519502     2  0.1964      0.646 0.056 0.944 0.000
#&gt; ERR519486     3  0.0000      0.973 0.000 0.000 1.000
#&gt; ERR519478     1  0.1031      0.413 0.976 0.024 0.000
#&gt; ERR519497     2  0.6192      0.328 0.420 0.580 0.000
#&gt; ERR519467     1  0.6095      0.762 0.608 0.392 0.000
#&gt; ERR519489     3  0.0000      0.973 0.000 0.000 1.000
#&gt; ERR519494     3  0.0000      0.973 0.000 0.000 1.000
#&gt; ERR519474     1  0.6126      0.760 0.600 0.400 0.000
#&gt; ERR519505     2  0.6274     -0.464 0.456 0.544 0.000
#&gt; ERR519517     3  0.0000      0.973 0.000 0.000 1.000
#&gt; ERR519484     2  0.6168     -0.312 0.412 0.588 0.000
#&gt; ERR519498     2  0.3482      0.593 0.128 0.872 0.000
#&gt; ERR519490     3  0.0000      0.973 0.000 0.000 1.000
#&gt; ERR519507     2  0.5497      0.218 0.292 0.708 0.000
#&gt; ERR519511     3  0.0000      0.973 0.000 0.000 1.000
#&gt; ERR519468     2  0.3805      0.576 0.024 0.884 0.092
#&gt; ERR519482     3  0.6578      0.746 0.224 0.052 0.724
#&gt; ERR519475     1  0.6126      0.760 0.600 0.400 0.000
#&gt; ERR519496     1  0.1964      0.325 0.944 0.056 0.000
#&gt; ERR519506     1  0.6126      0.760 0.600 0.400 0.000
#&gt; ERR519469     2  0.0237      0.639 0.004 0.996 0.000
#&gt; ERR519480     3  0.0000      0.973 0.000 0.000 1.000
#&gt; ERR519487     3  0.0000      0.973 0.000 0.000 1.000
#&gt; ERR519483     1  0.6859      0.727 0.620 0.356 0.024
#&gt; ERR519477     1  0.6126      0.760 0.600 0.400 0.000
#&gt; ERR519499     3  0.0000      0.973 0.000 0.000 1.000
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-2-a').click(function(){
  $('#tab-CV-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-3'>
<p><a id='tab-CV-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; ERR519515     1  0.2589    0.65750 0.884 0.116 0.000 0.000
#&gt; ERR519516     1  0.1388    0.69100 0.960 0.028 0.000 0.012
#&gt; ERR519520     2  0.4328    0.47982 0.244 0.748 0.000 0.008
#&gt; ERR519513     1  0.7860   -0.16823 0.396 0.292 0.000 0.312
#&gt; ERR519481     4  0.7818    0.14714 0.356 0.256 0.000 0.388
#&gt; ERR519491     1  0.0188    0.69782 0.996 0.004 0.000 0.000
#&gt; ERR519473     4  0.0000    0.50097 0.000 0.000 0.000 1.000
#&gt; ERR519518     2  0.5090    0.20669 0.000 0.728 0.044 0.228
#&gt; ERR519512     1  0.7148    0.25922 0.496 0.364 0.000 0.140
#&gt; ERR519521     2  0.7781   -0.23052 0.248 0.408 0.000 0.344
#&gt; ERR519488     1  0.4605    0.22957 0.664 0.336 0.000 0.000
#&gt; ERR519493     1  0.1256    0.69202 0.964 0.028 0.000 0.008
#&gt; ERR519514     1  0.2589    0.65750 0.884 0.116 0.000 0.000
#&gt; ERR519479     1  0.3679    0.64027 0.856 0.084 0.000 0.060
#&gt; ERR519509     2  0.4999    0.28915 0.492 0.508 0.000 0.000
#&gt; ERR519472     4  0.5250    0.08844 0.440 0.008 0.000 0.552
#&gt; ERR519510     1  0.6815    0.28508 0.580 0.284 0.000 0.136
#&gt; ERR519470     1  0.2647    0.65459 0.880 0.120 0.000 0.000
#&gt; ERR519495     4  0.4356    0.19751 0.000 0.000 0.292 0.708
#&gt; ERR519522     1  0.3266    0.60436 0.832 0.168 0.000 0.000
#&gt; ERR519523     1  0.2704    0.65563 0.876 0.124 0.000 0.000
#&gt; ERR519503     2  0.5178    0.53933 0.252 0.716 0.020 0.012
#&gt; ERR519471     1  0.2589    0.65750 0.884 0.116 0.000 0.000
#&gt; ERR519500     1  0.6060    0.00536 0.516 0.044 0.000 0.440
#&gt; ERR519485     1  0.2111    0.67496 0.932 0.024 0.000 0.044
#&gt; ERR519476     1  0.0000    0.69820 1.000 0.000 0.000 0.000
#&gt; ERR519502     4  0.7818    0.14714 0.356 0.256 0.000 0.388
#&gt; ERR519486     3  0.0000    0.95038 0.000 0.000 1.000 0.000
#&gt; ERR519478     2  0.4999    0.28915 0.492 0.508 0.000 0.000
#&gt; ERR519497     2  0.2676    0.31198 0.012 0.896 0.000 0.092
#&gt; ERR519467     1  0.2868    0.64115 0.864 0.136 0.000 0.000
#&gt; ERR519489     3  0.0000    0.95038 0.000 0.000 1.000 0.000
#&gt; ERR519494     3  0.0000    0.95038 0.000 0.000 1.000 0.000
#&gt; ERR519474     1  0.0000    0.69820 1.000 0.000 0.000 0.000
#&gt; ERR519505     1  0.6639    0.31599 0.596 0.284 0.000 0.120
#&gt; ERR519517     3  0.0000    0.95038 0.000 0.000 1.000 0.000
#&gt; ERR519484     1  0.6572    0.33213 0.608 0.272 0.000 0.120
#&gt; ERR519498     1  0.7086    0.21230 0.548 0.292 0.000 0.160
#&gt; ERR519490     3  0.0000    0.95038 0.000 0.000 1.000 0.000
#&gt; ERR519507     1  0.5069    0.36612 0.664 0.016 0.000 0.320
#&gt; ERR519511     3  0.0336    0.94380 0.000 0.008 0.992 0.000
#&gt; ERR519468     4  0.1820    0.48091 0.000 0.036 0.020 0.944
#&gt; ERR519482     3  0.6090    0.40085 0.000 0.384 0.564 0.052
#&gt; ERR519475     1  0.0000    0.69820 1.000 0.000 0.000 0.000
#&gt; ERR519496     2  0.4804    0.54270 0.276 0.708 0.000 0.016
#&gt; ERR519506     1  0.0188    0.69826 0.996 0.000 0.000 0.004
#&gt; ERR519469     4  0.0336    0.50069 0.000 0.008 0.000 0.992
#&gt; ERR519480     3  0.0000    0.95038 0.000 0.000 1.000 0.000
#&gt; ERR519487     3  0.0000    0.95038 0.000 0.000 1.000 0.000
#&gt; ERR519483     1  0.4734    0.47766 0.776 0.040 0.004 0.180
#&gt; ERR519477     1  0.0000    0.69820 1.000 0.000 0.000 0.000
#&gt; ERR519499     3  0.0000    0.95038 0.000 0.000 1.000 0.000
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-3-a').click(function(){
  $('#tab-CV-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-4'>
<p><a id='tab-CV-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; ERR519515     1  0.1251     0.7556 0.956 0.036 0.000 0.000 0.008
#&gt; ERR519516     1  0.3684     0.6244 0.720 0.000 0.000 0.000 0.280
#&gt; ERR519520     2  0.5354     0.4711 0.208 0.664 0.000 0.000 0.128
#&gt; ERR519513     5  0.2304     0.8120 0.068 0.004 0.000 0.020 0.908
#&gt; ERR519481     5  0.4651     0.7622 0.064 0.080 0.000 0.068 0.788
#&gt; ERR519491     1  0.1792     0.7664 0.916 0.000 0.000 0.000 0.084
#&gt; ERR519473     4  0.0404     0.7686 0.000 0.000 0.000 0.988 0.012
#&gt; ERR519518     2  0.3794     0.5996 0.000 0.832 0.016 0.080 0.072
#&gt; ERR519512     5  0.7100     0.1469 0.276 0.284 0.000 0.016 0.424
#&gt; ERR519521     5  0.3934     0.7128 0.020 0.092 0.000 0.064 0.824
#&gt; ERR519488     1  0.4878     0.4764 0.676 0.264 0.000 0.000 0.060
#&gt; ERR519493     1  0.2929     0.7234 0.820 0.000 0.000 0.000 0.180
#&gt; ERR519514     1  0.0880     0.7595 0.968 0.032 0.000 0.000 0.000
#&gt; ERR519479     1  0.4492     0.6111 0.712 0.016 0.000 0.016 0.256
#&gt; ERR519509     1  0.5454    -0.0330 0.488 0.452 0.000 0.000 0.060
#&gt; ERR519472     4  0.5617     0.0746 0.404 0.016 0.000 0.536 0.044
#&gt; ERR519510     5  0.2020     0.8082 0.100 0.000 0.000 0.000 0.900
#&gt; ERR519470     1  0.1043     0.7575 0.960 0.040 0.000 0.000 0.000
#&gt; ERR519495     4  0.1557     0.7482 0.000 0.008 0.052 0.940 0.000
#&gt; ERR519522     1  0.3930     0.6402 0.792 0.152 0.000 0.000 0.056
#&gt; ERR519523     1  0.2270     0.7458 0.904 0.076 0.000 0.000 0.020
#&gt; ERR519503     2  0.2020     0.6652 0.100 0.900 0.000 0.000 0.000
#&gt; ERR519471     1  0.1043     0.7575 0.960 0.040 0.000 0.000 0.000
#&gt; ERR519500     1  0.7472     0.1954 0.492 0.080 0.000 0.256 0.172
#&gt; ERR519485     1  0.1990     0.7694 0.920 0.008 0.000 0.004 0.068
#&gt; ERR519476     1  0.2280     0.7586 0.880 0.000 0.000 0.000 0.120
#&gt; ERR519502     5  0.4450     0.7567 0.052 0.084 0.000 0.064 0.800
#&gt; ERR519486     3  0.0000     0.9981 0.000 0.000 1.000 0.000 0.000
#&gt; ERR519478     1  0.5403    -0.0369 0.488 0.456 0.000 0.000 0.056
#&gt; ERR519497     2  0.2450     0.6400 0.000 0.896 0.000 0.028 0.076
#&gt; ERR519467     1  0.2983     0.7094 0.864 0.096 0.000 0.000 0.040
#&gt; ERR519489     3  0.0000     0.9981 0.000 0.000 1.000 0.000 0.000
#&gt; ERR519494     3  0.0000     0.9981 0.000 0.000 1.000 0.000 0.000
#&gt; ERR519474     1  0.2280     0.7572 0.880 0.000 0.000 0.000 0.120
#&gt; ERR519505     5  0.1851     0.8091 0.088 0.000 0.000 0.000 0.912
#&gt; ERR519517     3  0.0000     0.9981 0.000 0.000 1.000 0.000 0.000
#&gt; ERR519484     5  0.2605     0.7690 0.148 0.000 0.000 0.000 0.852
#&gt; ERR519498     5  0.1831     0.8150 0.076 0.000 0.000 0.004 0.920
#&gt; ERR519490     3  0.0000     0.9981 0.000 0.000 1.000 0.000 0.000
#&gt; ERR519507     1  0.5781     0.4661 0.620 0.008 0.000 0.260 0.112
#&gt; ERR519511     3  0.0404     0.9849 0.000 0.000 0.988 0.000 0.012
#&gt; ERR519468     4  0.1990     0.7406 0.000 0.040 0.028 0.928 0.004
#&gt; ERR519482     2  0.5310     0.0886 0.000 0.508 0.448 0.040 0.004
#&gt; ERR519475     1  0.2280     0.7586 0.880 0.000 0.000 0.000 0.120
#&gt; ERR519496     2  0.2773     0.6377 0.164 0.836 0.000 0.000 0.000
#&gt; ERR519506     1  0.2513     0.7585 0.876 0.000 0.000 0.008 0.116
#&gt; ERR519469     4  0.0324     0.7712 0.000 0.004 0.000 0.992 0.004
#&gt; ERR519480     3  0.0000     0.9981 0.000 0.000 1.000 0.000 0.000
#&gt; ERR519487     3  0.0000     0.9981 0.000 0.000 1.000 0.000 0.000
#&gt; ERR519483     1  0.5780     0.5839 0.672 0.028 0.000 0.180 0.120
#&gt; ERR519477     1  0.2280     0.7586 0.880 0.000 0.000 0.000 0.120
#&gt; ERR519499     3  0.0000     0.9981 0.000 0.000 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-4-a').click(function(){
  $('#tab-CV-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-5'>
<p><a id='tab-CV-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; ERR519515     1  0.2595     0.6639 0.836 0.000 0.000 0.160 0.000 0.004
#&gt; ERR519516     1  0.3974     0.5670 0.752 0.000 0.000 0.056 0.188 0.004
#&gt; ERR519520     4  0.5327     0.4466 0.096 0.000 0.000 0.668 0.048 0.188
#&gt; ERR519513     5  0.2756     0.8505 0.072 0.008 0.000 0.012 0.880 0.028
#&gt; ERR519481     5  0.3457     0.8022 0.016 0.028 0.000 0.064 0.848 0.044
#&gt; ERR519491     1  0.0935     0.7385 0.964 0.000 0.000 0.032 0.004 0.000
#&gt; ERR519473     2  0.1176     0.7146 0.000 0.956 0.000 0.020 0.024 0.000
#&gt; ERR519518     6  0.2489     0.7158 0.000 0.028 0.016 0.020 0.032 0.904
#&gt; ERR519512     4  0.6437     0.3526 0.096 0.004 0.000 0.572 0.196 0.132
#&gt; ERR519521     5  0.4934     0.6779 0.008 0.028 0.000 0.184 0.708 0.072
#&gt; ERR519488     4  0.4150     0.7231 0.320 0.000 0.000 0.652 0.000 0.028
#&gt; ERR519493     1  0.2290     0.7075 0.892 0.000 0.000 0.020 0.084 0.004
#&gt; ERR519514     1  0.2558     0.6677 0.840 0.000 0.000 0.156 0.000 0.004
#&gt; ERR519479     1  0.5141     0.5910 0.704 0.016 0.000 0.084 0.168 0.028
#&gt; ERR519509     4  0.4344     0.7355 0.304 0.000 0.000 0.652 0.000 0.044
#&gt; ERR519472     2  0.6350    -0.1036 0.416 0.440 0.000 0.084 0.044 0.016
#&gt; ERR519510     5  0.1765     0.8591 0.096 0.000 0.000 0.000 0.904 0.000
#&gt; ERR519470     1  0.2520     0.6697 0.844 0.000 0.000 0.152 0.000 0.004
#&gt; ERR519495     2  0.1262     0.7149 0.000 0.956 0.020 0.008 0.000 0.016
#&gt; ERR519522     4  0.3765     0.5668 0.404 0.000 0.000 0.596 0.000 0.000
#&gt; ERR519523     1  0.3652     0.6122 0.760 0.000 0.000 0.212 0.020 0.008
#&gt; ERR519503     6  0.3163     0.7073 0.004 0.000 0.000 0.232 0.000 0.764
#&gt; ERR519471     1  0.2558     0.6689 0.840 0.000 0.000 0.156 0.000 0.004
#&gt; ERR519500     1  0.7704     0.2156 0.468 0.200 0.000 0.152 0.128 0.052
#&gt; ERR519485     1  0.3706     0.6656 0.808 0.016 0.000 0.132 0.008 0.036
#&gt; ERR519476     1  0.0692     0.7381 0.976 0.000 0.000 0.004 0.020 0.000
#&gt; ERR519502     5  0.3322     0.8013 0.012 0.032 0.000 0.056 0.856 0.044
#&gt; ERR519486     3  0.1148     0.9548 0.000 0.004 0.960 0.020 0.000 0.016
#&gt; ERR519478     4  0.4499     0.7351 0.288 0.000 0.000 0.652 0.000 0.060
#&gt; ERR519497     6  0.3575     0.7292 0.000 0.000 0.000 0.128 0.076 0.796
#&gt; ERR519467     1  0.3765     0.0591 0.596 0.000 0.000 0.404 0.000 0.000
#&gt; ERR519489     3  0.0000     0.9839 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519494     3  0.0000     0.9839 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519474     1  0.1003     0.7379 0.964 0.000 0.000 0.016 0.020 0.000
#&gt; ERR519505     5  0.2333     0.8578 0.092 0.000 0.000 0.024 0.884 0.000
#&gt; ERR519517     3  0.0000     0.9839 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519484     5  0.2668     0.8024 0.168 0.000 0.000 0.004 0.828 0.000
#&gt; ERR519498     5  0.1812     0.8621 0.080 0.000 0.000 0.000 0.912 0.008
#&gt; ERR519490     3  0.0000     0.9839 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519507     1  0.6173     0.4414 0.608 0.220 0.000 0.092 0.056 0.024
#&gt; ERR519511     3  0.2457     0.9080 0.000 0.008 0.904 0.032 0.028 0.028
#&gt; ERR519468     2  0.3256     0.6522 0.000 0.836 0.020 0.032 0.000 0.112
#&gt; ERR519482     6  0.4320     0.5694 0.000 0.032 0.244 0.012 0.004 0.708
#&gt; ERR519475     1  0.0692     0.7381 0.976 0.000 0.000 0.004 0.020 0.000
#&gt; ERR519496     6  0.4385     0.6166 0.060 0.000 0.000 0.240 0.004 0.696
#&gt; ERR519506     1  0.1780     0.7319 0.932 0.004 0.000 0.036 0.024 0.004
#&gt; ERR519469     2  0.1675     0.7195 0.000 0.936 0.000 0.032 0.008 0.024
#&gt; ERR519480     3  0.0000     0.9839 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519487     3  0.0000     0.9839 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519483     1  0.6905     0.3979 0.580 0.092 0.012 0.200 0.044 0.072
#&gt; ERR519477     1  0.0692     0.7381 0.976 0.000 0.000 0.004 0.020 0.000
#&gt; ERR519499     3  0.0000     0.9839 0.000 0.000 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-5-a').click(function(){
  $('#tab-CV-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-CV-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-get-signatures'>
<ul>
<li><a href='#tab-CV-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-skmeans-signature_compare](figure_cola/CV-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-CV-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-skmeans-collect-classes](figure_cola/CV-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:pam**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "pam"]
# you can also extract it by
# res = res_list["CV:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 18140 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-pam-collect-plots](figure_cola/CV-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-pam-select-partition-number](figure_cola/CV-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.991       0.996          0.215 0.792   0.792
#> 3 3 0.964           0.882       0.969          0.248 0.966   0.957
#> 4 4 0.663           0.894       0.944          0.363 0.905   0.875
#> 5 5 0.488           0.628       0.857          0.318 0.934   0.901
#> 6 6 0.502           0.432       0.752          0.134 0.748   0.614
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-pam-get-classes'>
<ul>
<li><a href='#tab-CV-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-pam-get-classes-1'>
<p><a id='tab-CV-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; ERR519515     1    0.00      0.995 1.000 0.000
#&gt; ERR519516     1    0.00      0.995 1.000 0.000
#&gt; ERR519520     1    0.00      0.995 1.000 0.000
#&gt; ERR519513     1    0.00      0.995 1.000 0.000
#&gt; ERR519481     1    0.00      0.995 1.000 0.000
#&gt; ERR519491     1    0.00      0.995 1.000 0.000
#&gt; ERR519473     1    0.00      0.995 1.000 0.000
#&gt; ERR519518     1    0.00      0.995 1.000 0.000
#&gt; ERR519512     1    0.00      0.995 1.000 0.000
#&gt; ERR519521     1    0.00      0.995 1.000 0.000
#&gt; ERR519488     1    0.00      0.995 1.000 0.000
#&gt; ERR519493     1    0.00      0.995 1.000 0.000
#&gt; ERR519514     1    0.00      0.995 1.000 0.000
#&gt; ERR519479     1    0.00      0.995 1.000 0.000
#&gt; ERR519509     1    0.00      0.995 1.000 0.000
#&gt; ERR519472     1    0.00      0.995 1.000 0.000
#&gt; ERR519510     1    0.00      0.995 1.000 0.000
#&gt; ERR519470     1    0.00      0.995 1.000 0.000
#&gt; ERR519495     1    0.00      0.995 1.000 0.000
#&gt; ERR519522     1    0.00      0.995 1.000 0.000
#&gt; ERR519523     1    0.00      0.995 1.000 0.000
#&gt; ERR519503     1    0.00      0.995 1.000 0.000
#&gt; ERR519471     1    0.00      0.995 1.000 0.000
#&gt; ERR519500     1    0.00      0.995 1.000 0.000
#&gt; ERR519485     1    0.00      0.995 1.000 0.000
#&gt; ERR519476     1    0.00      0.995 1.000 0.000
#&gt; ERR519502     1    0.00      0.995 1.000 0.000
#&gt; ERR519486     1    0.00      0.995 1.000 0.000
#&gt; ERR519478     1    0.00      0.995 1.000 0.000
#&gt; ERR519497     1    0.00      0.995 1.000 0.000
#&gt; ERR519467     1    0.00      0.995 1.000 0.000
#&gt; ERR519489     2    0.00      1.000 0.000 1.000
#&gt; ERR519494     2    0.00      1.000 0.000 1.000
#&gt; ERR519474     1    0.00      0.995 1.000 0.000
#&gt; ERR519505     1    0.00      0.995 1.000 0.000
#&gt; ERR519517     2    0.00      1.000 0.000 1.000
#&gt; ERR519484     1    0.00      0.995 1.000 0.000
#&gt; ERR519498     1    0.00      0.995 1.000 0.000
#&gt; ERR519490     2    0.00      1.000 0.000 1.000
#&gt; ERR519507     1    0.00      0.995 1.000 0.000
#&gt; ERR519511     1    0.00      0.995 1.000 0.000
#&gt; ERR519468     1    0.00      0.995 1.000 0.000
#&gt; ERR519482     1    0.00      0.995 1.000 0.000
#&gt; ERR519475     1    0.00      0.995 1.000 0.000
#&gt; ERR519496     1    0.00      0.995 1.000 0.000
#&gt; ERR519506     1    0.00      0.995 1.000 0.000
#&gt; ERR519469     1    0.00      0.995 1.000 0.000
#&gt; ERR519480     1    0.73      0.744 0.796 0.204
#&gt; ERR519487     2    0.00      1.000 0.000 1.000
#&gt; ERR519483     1    0.00      0.995 1.000 0.000
#&gt; ERR519477     1    0.00      0.995 1.000 0.000
#&gt; ERR519499     2    0.00      1.000 0.000 1.000
</code></pre>

<script>
$('#tab-CV-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-1-a').click(function(){
  $('#tab-CV-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-2'>
<p><a id='tab-CV-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette  p1  p2 p3
#&gt; ERR519515     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519516     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519520     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519513     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519481     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519491     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519473     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519518     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519512     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519521     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519488     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519493     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519514     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519479     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519509     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519472     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519510     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519470     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519495     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519522     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519523     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519503     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519471     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519500     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519485     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519476     1   0.613    -0.0797 0.6 0.4  0
#&gt; ERR519502     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519486     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519478     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519497     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519467     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519489     3   0.000     1.0000 0.0 0.0  1
#&gt; ERR519494     3   0.000     1.0000 0.0 0.0  1
#&gt; ERR519474     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519505     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519517     3   0.000     1.0000 0.0 0.0  1
#&gt; ERR519484     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519498     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519490     3   0.000     1.0000 0.0 0.0  1
#&gt; ERR519507     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519511     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519468     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519482     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519475     1   0.613    -0.0797 0.6 0.4  0
#&gt; ERR519496     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519506     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519469     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519480     2   0.613     0.0000 0.4 0.6  0
#&gt; ERR519487     3   0.000     1.0000 0.0 0.0  1
#&gt; ERR519483     1   0.000     0.9545 1.0 0.0  0
#&gt; ERR519477     1   0.613    -0.0797 0.6 0.4  0
#&gt; ERR519499     3   0.000     1.0000 0.0 0.0  1
</code></pre>

<script>
$('#tab-CV-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-2-a').click(function(){
  $('#tab-CV-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-3'>
<p><a id='tab-CV-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3 p4
#&gt; ERR519515     1  0.0000      0.935 1.000 0.000 0.000  0
#&gt; ERR519516     1  0.0000      0.935 1.000 0.000 0.000  0
#&gt; ERR519520     1  0.3311      0.798 0.828 0.172 0.000  0
#&gt; ERR519513     1  0.0000      0.935 1.000 0.000 0.000  0
#&gt; ERR519481     1  0.0000      0.935 1.000 0.000 0.000  0
#&gt; ERR519491     1  0.0000      0.935 1.000 0.000 0.000  0
#&gt; ERR519473     1  0.0000      0.935 1.000 0.000 0.000  0
#&gt; ERR519518     1  0.3726      0.754 0.788 0.212 0.000  0
#&gt; ERR519512     1  0.1389      0.906 0.952 0.048 0.000  0
#&gt; ERR519521     1  0.2469      0.859 0.892 0.108 0.000  0
#&gt; ERR519488     1  0.2814      0.837 0.868 0.132 0.000  0
#&gt; ERR519493     1  0.0000      0.935 1.000 0.000 0.000  0
#&gt; ERR519514     1  0.0000      0.935 1.000 0.000 0.000  0
#&gt; ERR519479     1  0.0000      0.935 1.000 0.000 0.000  0
#&gt; ERR519509     1  0.3311      0.798 0.828 0.172 0.000  0
#&gt; ERR519472     1  0.0000      0.935 1.000 0.000 0.000  0
#&gt; ERR519510     1  0.0000      0.935 1.000 0.000 0.000  0
#&gt; ERR519470     1  0.0000      0.935 1.000 0.000 0.000  0
#&gt; ERR519495     1  0.0000      0.935 1.000 0.000 0.000  0
#&gt; ERR519522     1  0.0000      0.935 1.000 0.000 0.000  0
#&gt; ERR519523     1  0.0000      0.935 1.000 0.000 0.000  0
#&gt; ERR519503     1  0.3726      0.754 0.788 0.212 0.000  0
#&gt; ERR519471     1  0.0000      0.935 1.000 0.000 0.000  0
#&gt; ERR519500     1  0.0000      0.935 1.000 0.000 0.000  0
#&gt; ERR519485     1  0.0000      0.935 1.000 0.000 0.000  0
#&gt; ERR519476     2  0.4277      1.000 0.280 0.720 0.000  0
#&gt; ERR519502     1  0.0000      0.935 1.000 0.000 0.000  0
#&gt; ERR519486     1  0.0000      0.935 1.000 0.000 0.000  0
#&gt; ERR519478     1  0.3726      0.754 0.788 0.212 0.000  0
#&gt; ERR519497     1  0.3726      0.754 0.788 0.212 0.000  0
#&gt; ERR519467     1  0.0592      0.922 0.984 0.016 0.000  0
#&gt; ERR519489     3  0.0000      0.987 0.000 0.000 1.000  0
#&gt; ERR519494     3  0.0000      0.987 0.000 0.000 1.000  0
#&gt; ERR519474     1  0.1302      0.893 0.956 0.044 0.000  0
#&gt; ERR519505     1  0.1389      0.906 0.952 0.048 0.000  0
#&gt; ERR519517     3  0.0000      0.987 0.000 0.000 1.000  0
#&gt; ERR519484     1  0.0188      0.932 0.996 0.004 0.000  0
#&gt; ERR519498     1  0.0000      0.935 1.000 0.000 0.000  0
#&gt; ERR519490     3  0.1792      0.934 0.000 0.068 0.932  0
#&gt; ERR519507     1  0.0000      0.935 1.000 0.000 0.000  0
#&gt; ERR519511     1  0.1022      0.914 0.968 0.032 0.000  0
#&gt; ERR519468     1  0.0000      0.935 1.000 0.000 0.000  0
#&gt; ERR519482     1  0.3688      0.759 0.792 0.208 0.000  0
#&gt; ERR519475     2  0.4277      1.000 0.280 0.720 0.000  0
#&gt; ERR519496     1  0.3569      0.771 0.804 0.196 0.000  0
#&gt; ERR519506     1  0.0000      0.935 1.000 0.000 0.000  0
#&gt; ERR519469     1  0.0000      0.935 1.000 0.000 0.000  0
#&gt; ERR519480     4  0.0000      0.000 0.000 0.000 0.000  1
#&gt; ERR519487     3  0.0000      0.987 0.000 0.000 1.000  0
#&gt; ERR519483     1  0.0000      0.935 1.000 0.000 0.000  0
#&gt; ERR519477     2  0.4277      1.000 0.280 0.720 0.000  0
#&gt; ERR519499     3  0.0000      0.987 0.000 0.000 1.000  0
</code></pre>

<script>
$('#tab-CV-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-3-a').click(function(){
  $('#tab-CV-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-4'>
<p><a id='tab-CV-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4 p5
#&gt; ERR519515     1  0.0000     0.7937 1.000 0.000 0.000 0.000  0
#&gt; ERR519516     1  0.0000     0.7937 1.000 0.000 0.000 0.000  0
#&gt; ERR519520     1  0.3381     0.6228 0.808 0.176 0.000 0.016  0
#&gt; ERR519513     1  0.4182     0.1965 0.600 0.000 0.000 0.400  0
#&gt; ERR519481     1  0.4182     0.1965 0.600 0.000 0.000 0.400  0
#&gt; ERR519491     1  0.0000     0.7937 1.000 0.000 0.000 0.000  0
#&gt; ERR519473     1  0.0000     0.7937 1.000 0.000 0.000 0.000  0
#&gt; ERR519518     4  0.6622     0.2939 0.364 0.220 0.000 0.416  0
#&gt; ERR519512     1  0.1774     0.7498 0.932 0.052 0.000 0.016  0
#&gt; ERR519521     1  0.5537     0.2959 0.624 0.112 0.000 0.264  0
#&gt; ERR519488     1  0.2920     0.6747 0.852 0.132 0.000 0.016  0
#&gt; ERR519493     1  0.0794     0.7786 0.972 0.000 0.000 0.028  0
#&gt; ERR519514     1  0.0000     0.7937 1.000 0.000 0.000 0.000  0
#&gt; ERR519479     1  0.0290     0.7902 0.992 0.000 0.000 0.008  0
#&gt; ERR519509     1  0.3381     0.6228 0.808 0.176 0.000 0.016  0
#&gt; ERR519472     1  0.0000     0.7937 1.000 0.000 0.000 0.000  0
#&gt; ERR519510     1  0.4182     0.1965 0.600 0.000 0.000 0.400  0
#&gt; ERR519470     1  0.0000     0.7937 1.000 0.000 0.000 0.000  0
#&gt; ERR519495     1  0.0000     0.7937 1.000 0.000 0.000 0.000  0
#&gt; ERR519522     1  0.0000     0.7937 1.000 0.000 0.000 0.000  0
#&gt; ERR519523     1  0.0000     0.7937 1.000 0.000 0.000 0.000  0
#&gt; ERR519503     1  0.3759     0.5603 0.764 0.220 0.000 0.016  0
#&gt; ERR519471     1  0.0000     0.7937 1.000 0.000 0.000 0.000  0
#&gt; ERR519500     1  0.0000     0.7937 1.000 0.000 0.000 0.000  0
#&gt; ERR519485     1  0.0000     0.7937 1.000 0.000 0.000 0.000  0
#&gt; ERR519476     2  0.3274     1.0000 0.220 0.780 0.000 0.000  0
#&gt; ERR519502     1  0.4182     0.1965 0.600 0.000 0.000 0.400  0
#&gt; ERR519486     1  0.2068     0.7227 0.904 0.004 0.000 0.092  0
#&gt; ERR519478     1  0.3727     0.5664 0.768 0.216 0.000 0.016  0
#&gt; ERR519497     4  0.6622     0.2939 0.364 0.220 0.000 0.416  0
#&gt; ERR519467     1  0.0609     0.7812 0.980 0.020 0.000 0.000  0
#&gt; ERR519489     3  0.0000     1.0000 0.000 0.000 1.000 0.000  0
#&gt; ERR519494     3  0.0000     1.0000 0.000 0.000 1.000 0.000  0
#&gt; ERR519474     1  0.1341     0.7521 0.944 0.056 0.000 0.000  0
#&gt; ERR519505     1  0.5250     0.0211 0.536 0.048 0.000 0.416  0
#&gt; ERR519517     3  0.0000     1.0000 0.000 0.000 1.000 0.000  0
#&gt; ERR519484     1  0.4331     0.1874 0.596 0.004 0.000 0.400  0
#&gt; ERR519498     1  0.4182     0.1965 0.600 0.000 0.000 0.400  0
#&gt; ERR519490     4  0.4219    -0.6280 0.000 0.000 0.416 0.584  0
#&gt; ERR519507     1  0.0000     0.7937 1.000 0.000 0.000 0.000  0
#&gt; ERR519511     1  0.5028     0.0911 0.564 0.036 0.000 0.400  0
#&gt; ERR519468     1  0.0000     0.7937 1.000 0.000 0.000 0.000  0
#&gt; ERR519482     1  0.3519     0.5796 0.776 0.216 0.000 0.008  0
#&gt; ERR519475     2  0.3274     1.0000 0.220 0.780 0.000 0.000  0
#&gt; ERR519496     1  0.3109     0.6089 0.800 0.200 0.000 0.000  0
#&gt; ERR519506     1  0.0000     0.7937 1.000 0.000 0.000 0.000  0
#&gt; ERR519469     1  0.0000     0.7937 1.000 0.000 0.000 0.000  0
#&gt; ERR519480     5  0.0000     0.0000 0.000 0.000 0.000 0.000  1
#&gt; ERR519487     3  0.0000     1.0000 0.000 0.000 1.000 0.000  0
#&gt; ERR519483     1  0.0000     0.7937 1.000 0.000 0.000 0.000  0
#&gt; ERR519477     2  0.3274     1.0000 0.220 0.780 0.000 0.000  0
#&gt; ERR519499     3  0.0000     1.0000 0.000 0.000 1.000 0.000  0
</code></pre>

<script>
$('#tab-CV-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-4-a').click(function(){
  $('#tab-CV-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-5'>
<p><a id='tab-CV-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3 p4    p5    p6
#&gt; ERR519515     5  0.3930     0.4475 0.420 0.004 0.000  0 0.576 0.000
#&gt; ERR519516     5  0.3930     0.4475 0.420 0.004 0.000  0 0.576 0.000
#&gt; ERR519520     1  0.2996     0.7761 0.772 0.000 0.000  0 0.228 0.000
#&gt; ERR519513     5  0.0000     0.2339 0.000 0.000 0.000  0 1.000 0.000
#&gt; ERR519481     5  0.0146     0.2332 0.000 0.004 0.000  0 0.996 0.000
#&gt; ERR519491     5  0.3930     0.4475 0.420 0.004 0.000  0 0.576 0.000
#&gt; ERR519473     5  0.3797     0.4480 0.420 0.000 0.000  0 0.580 0.000
#&gt; ERR519518     5  0.3789    -0.3735 0.416 0.000 0.000  0 0.584 0.000
#&gt; ERR519512     1  0.3531     0.6135 0.672 0.000 0.000  0 0.328 0.000
#&gt; ERR519521     5  0.3843    -0.3019 0.452 0.000 0.000  0 0.548 0.000
#&gt; ERR519488     1  0.3592     0.6067 0.656 0.000 0.000  0 0.344 0.000
#&gt; ERR519493     5  0.3872     0.4195 0.392 0.004 0.000  0 0.604 0.000
#&gt; ERR519514     5  0.3930     0.4475 0.420 0.004 0.000  0 0.576 0.000
#&gt; ERR519479     5  0.3782     0.4423 0.412 0.000 0.000  0 0.588 0.000
#&gt; ERR519509     1  0.2996     0.7761 0.772 0.000 0.000  0 0.228 0.000
#&gt; ERR519472     5  0.3797     0.4480 0.420 0.000 0.000  0 0.580 0.000
#&gt; ERR519510     5  0.0000     0.2339 0.000 0.000 0.000  0 1.000 0.000
#&gt; ERR519470     5  0.3930     0.4475 0.420 0.004 0.000  0 0.576 0.000
#&gt; ERR519495     5  0.3797     0.4480 0.420 0.000 0.000  0 0.580 0.000
#&gt; ERR519522     5  0.3930     0.4475 0.420 0.004 0.000  0 0.576 0.000
#&gt; ERR519523     5  0.3930     0.4475 0.420 0.004 0.000  0 0.576 0.000
#&gt; ERR519503     1  0.2491     0.7149 0.836 0.000 0.000  0 0.164 0.000
#&gt; ERR519471     5  0.3930     0.4475 0.420 0.004 0.000  0 0.576 0.000
#&gt; ERR519500     5  0.3797     0.4480 0.420 0.000 0.000  0 0.580 0.000
#&gt; ERR519485     5  0.3797     0.4480 0.420 0.000 0.000  0 0.580 0.000
#&gt; ERR519476     2  0.2762     1.0000 0.000 0.804 0.000  0 0.196 0.000
#&gt; ERR519502     5  0.0000     0.2339 0.000 0.000 0.000  0 1.000 0.000
#&gt; ERR519486     5  0.3592     0.2850 0.344 0.000 0.000  0 0.656 0.000
#&gt; ERR519478     1  0.2697     0.7482 0.812 0.000 0.000  0 0.188 0.000
#&gt; ERR519497     5  0.3789    -0.3735 0.416 0.000 0.000  0 0.584 0.000
#&gt; ERR519467     5  0.4355     0.4055 0.420 0.024 0.000  0 0.556 0.000
#&gt; ERR519489     3  0.2178     0.7842 0.000 0.132 0.868  0 0.000 0.000
#&gt; ERR519494     3  0.0000     0.8580 0.000 0.000 1.000  0 0.000 0.000
#&gt; ERR519474     5  0.4921     0.2978 0.420 0.064 0.000  0 0.516 0.000
#&gt; ERR519505     5  0.2941    -0.0523 0.220 0.000 0.000  0 0.780 0.000
#&gt; ERR519517     3  0.0000     0.8580 0.000 0.000 1.000  0 0.000 0.000
#&gt; ERR519484     5  0.0260     0.2304 0.000 0.008 0.000  0 0.992 0.000
#&gt; ERR519498     5  0.0000     0.2339 0.000 0.000 0.000  0 1.000 0.000
#&gt; ERR519490     3  0.6737     0.1614 0.164 0.064 0.396  0 0.000 0.376
#&gt; ERR519507     5  0.3797     0.4480 0.420 0.000 0.000  0 0.580 0.000
#&gt; ERR519511     5  0.1204     0.1780 0.056 0.000 0.000  0 0.944 0.000
#&gt; ERR519468     5  0.3797     0.4480 0.420 0.000 0.000  0 0.580 0.000
#&gt; ERR519482     6  0.5055     0.0000 0.244 0.000 0.000  0 0.132 0.624
#&gt; ERR519475     2  0.2762     1.0000 0.000 0.804 0.000  0 0.196 0.000
#&gt; ERR519496     1  0.3647     0.4453 0.640 0.000 0.000  0 0.360 0.000
#&gt; ERR519506     5  0.3930     0.4475 0.420 0.004 0.000  0 0.576 0.000
#&gt; ERR519469     5  0.3797     0.4480 0.420 0.000 0.000  0 0.580 0.000
#&gt; ERR519480     4  0.0000     0.0000 0.000 0.000 0.000  1 0.000 0.000
#&gt; ERR519487     3  0.0000     0.8580 0.000 0.000 1.000  0 0.000 0.000
#&gt; ERR519483     5  0.3797     0.4480 0.420 0.000 0.000  0 0.580 0.000
#&gt; ERR519477     2  0.2762     1.0000 0.000 0.804 0.000  0 0.196 0.000
#&gt; ERR519499     3  0.0000     0.8580 0.000 0.000 1.000  0 0.000 0.000
</code></pre>

<script>
$('#tab-CV-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-5-a').click(function(){
  $('#tab-CV-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-pam-membership-heatmap'>
<ul>
<li><a href='#tab-CV-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-pam-get-signatures'>
<ul>
<li><a href='#tab-CV-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-1-1.png" alt="plot of chunk tab-CV-pam-get-signatures-1"/></p>

</div>
<div id='tab-CV-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-2-1.png" alt="plot of chunk tab-CV-pam-get-signatures-2"/></p>

</div>
<div id='tab-CV-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-3-1.png" alt="plot of chunk tab-CV-pam-get-signatures-3"/></p>

</div>
<div id='tab-CV-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-4-1.png" alt="plot of chunk tab-CV-pam-get-signatures-4"/></p>

</div>
<div id='tab-CV-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-5-1.png" alt="plot of chunk tab-CV-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-pam-signature_compare](figure_cola/CV-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-pam-dimension-reduction'>
<ul>
<li><a href='#tab-CV-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-pam-collect-classes](figure_cola/CV-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:mclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "mclust"]
# you can also extract it by
# res = res_list["CV:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 18140 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-mclust-collect-plots](figure_cola/CV-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-mclust-select-partition-number](figure_cola/CV-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.962           0.950       0.980         0.2905 0.708   0.708
#> 3 3 0.350           0.316       0.686         0.7175 0.630   0.508
#> 4 4 0.264           0.592       0.736         0.0516 0.623   0.484
#> 5 5 0.345           0.452       0.739         0.1320 0.780   0.673
#> 6 6 0.331           0.409       0.697         0.1467 0.723   0.492
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-get-classes'>
<ul>
<li><a href='#tab-CV-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-mclust-get-classes-1'>
<p><a id='tab-CV-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; ERR519515     1  0.0000      0.987 1.000 0.000
#&gt; ERR519516     1  0.0000      0.987 1.000 0.000
#&gt; ERR519520     1  0.0000      0.987 1.000 0.000
#&gt; ERR519513     1  0.0000      0.987 1.000 0.000
#&gt; ERR519481     1  0.0000      0.987 1.000 0.000
#&gt; ERR519491     1  0.0000      0.987 1.000 0.000
#&gt; ERR519473     1  0.0000      0.987 1.000 0.000
#&gt; ERR519518     2  0.9129      0.539 0.328 0.672
#&gt; ERR519512     1  0.0000      0.987 1.000 0.000
#&gt; ERR519521     1  0.0000      0.987 1.000 0.000
#&gt; ERR519488     1  0.0000      0.987 1.000 0.000
#&gt; ERR519493     1  0.0000      0.987 1.000 0.000
#&gt; ERR519514     1  0.0000      0.987 1.000 0.000
#&gt; ERR519479     1  0.0000      0.987 1.000 0.000
#&gt; ERR519509     1  0.0000      0.987 1.000 0.000
#&gt; ERR519472     1  0.0000      0.987 1.000 0.000
#&gt; ERR519510     1  0.0000      0.987 1.000 0.000
#&gt; ERR519470     1  0.0000      0.987 1.000 0.000
#&gt; ERR519495     1  0.0000      0.987 1.000 0.000
#&gt; ERR519522     1  0.0000      0.987 1.000 0.000
#&gt; ERR519523     1  0.0000      0.987 1.000 0.000
#&gt; ERR519503     1  0.9522      0.345 0.628 0.372
#&gt; ERR519471     1  0.0000      0.987 1.000 0.000
#&gt; ERR519500     1  0.0000      0.987 1.000 0.000
#&gt; ERR519485     1  0.0000      0.987 1.000 0.000
#&gt; ERR519476     1  0.0000      0.987 1.000 0.000
#&gt; ERR519502     1  0.0000      0.987 1.000 0.000
#&gt; ERR519486     1  0.0938      0.976 0.988 0.012
#&gt; ERR519478     1  0.0000      0.987 1.000 0.000
#&gt; ERR519497     1  0.1184      0.972 0.984 0.016
#&gt; ERR519467     1  0.0000      0.987 1.000 0.000
#&gt; ERR519489     2  0.0000      0.930 0.000 1.000
#&gt; ERR519494     2  0.0000      0.930 0.000 1.000
#&gt; ERR519474     1  0.0000      0.987 1.000 0.000
#&gt; ERR519505     1  0.0000      0.987 1.000 0.000
#&gt; ERR519517     2  0.0000      0.930 0.000 1.000
#&gt; ERR519484     1  0.0000      0.987 1.000 0.000
#&gt; ERR519498     1  0.0000      0.987 1.000 0.000
#&gt; ERR519490     2  0.0000      0.930 0.000 1.000
#&gt; ERR519507     1  0.0000      0.987 1.000 0.000
#&gt; ERR519511     1  0.0000      0.987 1.000 0.000
#&gt; ERR519468     1  0.0000      0.987 1.000 0.000
#&gt; ERR519482     2  0.7453      0.737 0.212 0.788
#&gt; ERR519475     1  0.0000      0.987 1.000 0.000
#&gt; ERR519496     1  0.0938      0.976 0.988 0.012
#&gt; ERR519506     1  0.0000      0.987 1.000 0.000
#&gt; ERR519469     1  0.0000      0.987 1.000 0.000
#&gt; ERR519480     2  0.0000      0.930 0.000 1.000
#&gt; ERR519487     2  0.0000      0.930 0.000 1.000
#&gt; ERR519483     1  0.4815      0.871 0.896 0.104
#&gt; ERR519477     1  0.0000      0.987 1.000 0.000
#&gt; ERR519499     2  0.0000      0.930 0.000 1.000
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-1-a').click(function(){
  $('#tab-CV-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-2'>
<p><a id='tab-CV-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; ERR519515     1  0.6309     0.1040 0.500 0.500 0.000
#&gt; ERR519516     1  0.6267     0.2036 0.548 0.452 0.000
#&gt; ERR519520     1  0.0592     0.2638 0.988 0.012 0.000
#&gt; ERR519513     1  0.6140     0.2363 0.596 0.404 0.000
#&gt; ERR519481     1  0.5882     0.2680 0.652 0.348 0.000
#&gt; ERR519491     2  0.6308    -0.1823 0.492 0.508 0.000
#&gt; ERR519473     2  0.6302     0.2943 0.480 0.520 0.000
#&gt; ERR519518     1  0.5012     0.2017 0.840 0.080 0.080
#&gt; ERR519512     1  0.5968     0.2650 0.636 0.364 0.000
#&gt; ERR519521     1  0.0237     0.2633 0.996 0.004 0.000
#&gt; ERR519488     1  0.6168     0.0764 0.588 0.412 0.000
#&gt; ERR519493     1  0.6267     0.2070 0.548 0.452 0.000
#&gt; ERR519514     2  0.6309    -0.1798 0.496 0.504 0.000
#&gt; ERR519479     1  0.6154     0.2331 0.592 0.408 0.000
#&gt; ERR519509     1  0.4346     0.1922 0.816 0.184 0.000
#&gt; ERR519472     2  0.6260     0.3147 0.448 0.552 0.000
#&gt; ERR519510     1  0.6180     0.2292 0.584 0.416 0.000
#&gt; ERR519470     1  0.6308     0.1216 0.508 0.492 0.000
#&gt; ERR519495     2  0.5138     0.5185 0.252 0.748 0.000
#&gt; ERR519522     1  0.6295     0.1361 0.528 0.472 0.000
#&gt; ERR519523     1  0.6225     0.2205 0.568 0.432 0.000
#&gt; ERR519503     1  0.5378     0.1214 0.756 0.236 0.008
#&gt; ERR519471     1  0.6307     0.1339 0.512 0.488 0.000
#&gt; ERR519500     1  0.6168     0.1785 0.588 0.412 0.000
#&gt; ERR519485     2  0.4842     0.5253 0.224 0.776 0.000
#&gt; ERR519476     2  0.4953     0.5031 0.176 0.808 0.016
#&gt; ERR519502     1  0.5988     0.2604 0.632 0.368 0.000
#&gt; ERR519486     2  0.6224     0.4869 0.240 0.728 0.032
#&gt; ERR519478     1  0.3482     0.2350 0.872 0.128 0.000
#&gt; ERR519497     1  0.0592     0.2614 0.988 0.012 0.000
#&gt; ERR519467     2  0.6252     0.0458 0.444 0.556 0.000
#&gt; ERR519489     3  0.0000     0.9546 0.000 0.000 1.000
#&gt; ERR519494     3  0.0000     0.9546 0.000 0.000 1.000
#&gt; ERR519474     1  0.6260     0.1979 0.552 0.448 0.000
#&gt; ERR519505     1  0.6299    -0.0397 0.524 0.476 0.000
#&gt; ERR519517     3  0.0000     0.9546 0.000 0.000 1.000
#&gt; ERR519484     1  0.6307    -0.0131 0.512 0.488 0.000
#&gt; ERR519498     1  0.6111     0.2450 0.604 0.396 0.000
#&gt; ERR519490     3  0.8357     0.7157 0.232 0.148 0.620
#&gt; ERR519507     2  0.6309     0.1521 0.496 0.504 0.000
#&gt; ERR519511     2  0.5926     0.4126 0.356 0.644 0.000
#&gt; ERR519468     1  0.6209     0.2519 0.628 0.368 0.004
#&gt; ERR519482     1  0.7775    -0.1813 0.620 0.076 0.304
#&gt; ERR519475     2  0.4953     0.5031 0.176 0.808 0.016
#&gt; ERR519496     1  0.4452     0.1361 0.808 0.192 0.000
#&gt; ERR519506     2  0.6204     0.3217 0.424 0.576 0.000
#&gt; ERR519469     1  0.5968     0.2606 0.636 0.364 0.000
#&gt; ERR519480     3  0.1163     0.9464 0.000 0.028 0.972
#&gt; ERR519487     3  0.0000     0.9546 0.000 0.000 1.000
#&gt; ERR519483     2  0.6099     0.4968 0.228 0.740 0.032
#&gt; ERR519477     2  0.4953     0.5031 0.176 0.808 0.016
#&gt; ERR519499     3  0.0000     0.9546 0.000 0.000 1.000
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-2-a').click(function(){
  $('#tab-CV-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-3'>
<p><a id='tab-CV-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; ERR519515     1  0.4123      0.682 0.772 0.220 0.000 0.008
#&gt; ERR519516     1  0.4244      0.685 0.800 0.168 0.000 0.032
#&gt; ERR519520     1  0.3306      0.568 0.840 0.004 0.000 0.156
#&gt; ERR519513     1  0.2408      0.680 0.920 0.044 0.000 0.036
#&gt; ERR519481     1  0.3249      0.616 0.852 0.008 0.000 0.140
#&gt; ERR519491     1  0.3768      0.689 0.808 0.184 0.000 0.008
#&gt; ERR519473     1  0.5116      0.605 0.764 0.128 0.000 0.108
#&gt; ERR519518     4  0.5398      0.559 0.404 0.000 0.016 0.580
#&gt; ERR519512     1  0.2593      0.644 0.892 0.004 0.000 0.104
#&gt; ERR519521     1  0.4220      0.448 0.748 0.004 0.000 0.248
#&gt; ERR519488     1  0.5574      0.646 0.668 0.284 0.000 0.048
#&gt; ERR519493     1  0.3718      0.688 0.820 0.168 0.000 0.012
#&gt; ERR519514     1  0.3610      0.702 0.800 0.200 0.000 0.000
#&gt; ERR519479     1  0.2271      0.707 0.916 0.076 0.000 0.008
#&gt; ERR519509     1  0.6617      0.544 0.608 0.264 0.000 0.128
#&gt; ERR519472     1  0.4070      0.651 0.824 0.132 0.000 0.044
#&gt; ERR519510     1  0.2271      0.700 0.916 0.076 0.000 0.008
#&gt; ERR519470     1  0.4391      0.672 0.740 0.252 0.000 0.008
#&gt; ERR519495     1  0.4933      0.595 0.688 0.296 0.000 0.016
#&gt; ERR519522     1  0.5627      0.649 0.692 0.240 0.000 0.068
#&gt; ERR519523     1  0.3161      0.705 0.864 0.124 0.000 0.012
#&gt; ERR519503     4  0.7186      0.415 0.420 0.136 0.000 0.444
#&gt; ERR519471     1  0.4194      0.688 0.800 0.172 0.000 0.028
#&gt; ERR519500     1  0.2408      0.681 0.920 0.036 0.000 0.044
#&gt; ERR519485     1  0.4762      0.594 0.692 0.300 0.004 0.004
#&gt; ERR519476     1  0.8062      0.355 0.472 0.244 0.016 0.268
#&gt; ERR519502     1  0.1940      0.660 0.924 0.000 0.000 0.076
#&gt; ERR519486     1  0.5360      0.577 0.668 0.304 0.024 0.004
#&gt; ERR519478     1  0.7224      0.356 0.548 0.236 0.000 0.216
#&gt; ERR519497     1  0.4543      0.130 0.676 0.000 0.000 0.324
#&gt; ERR519467     1  0.4522      0.659 0.680 0.320 0.000 0.000
#&gt; ERR519489     3  0.1151      0.948 0.000 0.008 0.968 0.024
#&gt; ERR519494     3  0.0188      0.979 0.000 0.004 0.996 0.000
#&gt; ERR519474     1  0.3311      0.696 0.828 0.172 0.000 0.000
#&gt; ERR519505     1  0.4152      0.705 0.808 0.160 0.000 0.032
#&gt; ERR519517     3  0.0672      0.975 0.000 0.008 0.984 0.008
#&gt; ERR519484     1  0.3757      0.708 0.828 0.152 0.000 0.020
#&gt; ERR519498     1  0.2319      0.680 0.924 0.036 0.000 0.040
#&gt; ERR519490     4  0.6477     -0.489 0.000 0.072 0.420 0.508
#&gt; ERR519507     1  0.3024      0.667 0.852 0.148 0.000 0.000
#&gt; ERR519511     1  0.4304      0.599 0.716 0.284 0.000 0.000
#&gt; ERR519468     1  0.3257      0.618 0.844 0.004 0.000 0.152
#&gt; ERR519482     4  0.6407      0.534 0.332 0.000 0.084 0.584
#&gt; ERR519475     1  0.8062      0.355 0.472 0.244 0.016 0.268
#&gt; ERR519496     1  0.6751      0.117 0.592 0.136 0.000 0.272
#&gt; ERR519506     1  0.4741      0.657 0.668 0.328 0.000 0.004
#&gt; ERR519469     1  0.2888      0.630 0.872 0.004 0.000 0.124
#&gt; ERR519480     2  0.7392      0.000 0.000 0.520 0.232 0.248
#&gt; ERR519487     3  0.0188      0.977 0.000 0.004 0.996 0.000
#&gt; ERR519483     1  0.6560      0.545 0.616 0.288 0.008 0.088
#&gt; ERR519477     1  0.8062      0.355 0.472 0.244 0.016 0.268
#&gt; ERR519499     3  0.0376      0.978 0.000 0.004 0.992 0.004
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-3-a').click(function(){
  $('#tab-CV-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-4'>
<p><a id='tab-CV-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; ERR519515     1   0.278      0.643 0.864 0.000 0.000 0.016 0.120
#&gt; ERR519516     1   0.427      0.627 0.776 0.000 0.000 0.116 0.108
#&gt; ERR519520     4   0.410      0.248 0.332 0.000 0.000 0.664 0.004
#&gt; ERR519513     1   0.304      0.629 0.808 0.000 0.000 0.192 0.000
#&gt; ERR519481     1   0.430      0.201 0.516 0.000 0.000 0.484 0.000
#&gt; ERR519491     1   0.291      0.644 0.860 0.000 0.000 0.024 0.116
#&gt; ERR519473     1   0.464      0.248 0.528 0.000 0.000 0.460 0.012
#&gt; ERR519518     4   0.511     -0.151 0.020 0.012 0.000 0.556 0.412
#&gt; ERR519512     1   0.432      0.431 0.600 0.000 0.000 0.396 0.004
#&gt; ERR519521     4   0.212      0.111 0.096 0.000 0.000 0.900 0.004
#&gt; ERR519488     1   0.527      0.421 0.680 0.000 0.000 0.172 0.148
#&gt; ERR519493     1   0.306      0.651 0.856 0.000 0.000 0.036 0.108
#&gt; ERR519514     1   0.304      0.656 0.860 0.000 0.000 0.040 0.100
#&gt; ERR519479     1   0.150      0.682 0.940 0.000 0.000 0.056 0.004
#&gt; ERR519509     4   0.630      0.201 0.424 0.000 0.000 0.424 0.152
#&gt; ERR519472     1   0.373      0.573 0.748 0.000 0.000 0.244 0.008
#&gt; ERR519510     1   0.229      0.663 0.888 0.000 0.000 0.108 0.004
#&gt; ERR519470     1   0.336      0.640 0.832 0.000 0.000 0.036 0.132
#&gt; ERR519495     1   0.415      0.634 0.780 0.000 0.000 0.144 0.076
#&gt; ERR519522     1   0.472      0.574 0.736 0.000 0.000 0.124 0.140
#&gt; ERR519523     1   0.285      0.654 0.840 0.000 0.000 0.156 0.004
#&gt; ERR519503     5   0.677     -0.396 0.360 0.000 0.000 0.272 0.368
#&gt; ERR519471     1   0.375      0.646 0.816 0.000 0.000 0.080 0.104
#&gt; ERR519500     1   0.328      0.628 0.804 0.000 0.000 0.188 0.008
#&gt; ERR519485     1   0.395      0.642 0.800 0.000 0.000 0.080 0.120
#&gt; ERR519476     1   0.661      0.256 0.512 0.212 0.000 0.008 0.268
#&gt; ERR519502     1   0.425      0.297 0.568 0.000 0.000 0.432 0.000
#&gt; ERR519486     1   0.418      0.603 0.744 0.000 0.000 0.036 0.220
#&gt; ERR519478     4   0.610      0.211 0.436 0.000 0.000 0.440 0.124
#&gt; ERR519497     4   0.437      0.247 0.372 0.000 0.000 0.620 0.008
#&gt; ERR519467     1   0.249      0.645 0.872 0.000 0.000 0.004 0.124
#&gt; ERR519489     3   0.000      1.000 0.000 0.000 1.000 0.000 0.000
#&gt; ERR519494     3   0.000      1.000 0.000 0.000 1.000 0.000 0.000
#&gt; ERR519474     1   0.346      0.654 0.832 0.000 0.000 0.052 0.116
#&gt; ERR519505     1   0.158      0.680 0.944 0.000 0.000 0.032 0.024
#&gt; ERR519517     3   0.000      1.000 0.000 0.000 1.000 0.000 0.000
#&gt; ERR519484     1   0.112      0.682 0.960 0.000 0.000 0.036 0.004
#&gt; ERR519498     1   0.307      0.621 0.804 0.000 0.000 0.196 0.000
#&gt; ERR519490     5   0.612     -0.427 0.000 0.128 0.412 0.000 0.460
#&gt; ERR519507     1   0.313      0.653 0.848 0.000 0.000 0.120 0.032
#&gt; ERR519511     1   0.384      0.645 0.808 0.000 0.000 0.116 0.076
#&gt; ERR519468     4   0.444     -0.261 0.472 0.000 0.000 0.524 0.004
#&gt; ERR519482     4   0.537     -0.160 0.020 0.024 0.000 0.544 0.412
#&gt; ERR519475     1   0.661      0.256 0.512 0.212 0.000 0.008 0.268
#&gt; ERR519496     4   0.500      0.227 0.364 0.000 0.000 0.596 0.040
#&gt; ERR519506     1   0.181      0.677 0.928 0.000 0.000 0.012 0.060
#&gt; ERR519469     4   0.456     -0.267 0.484 0.000 0.000 0.508 0.008
#&gt; ERR519480     2   0.141      0.000 0.000 0.940 0.000 0.000 0.060
#&gt; ERR519487     3   0.000      1.000 0.000 0.000 1.000 0.000 0.000
#&gt; ERR519483     1   0.508      0.533 0.664 0.004 0.000 0.060 0.272
#&gt; ERR519477     1   0.661      0.256 0.512 0.212 0.000 0.008 0.268
#&gt; ERR519499     3   0.000      1.000 0.000 0.000 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-4-a').click(function(){
  $('#tab-CV-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-5'>
<p><a id='tab-CV-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; ERR519515     1  0.3409     0.4712 0.700 0.000 0.000 0.000 0.300 0.000
#&gt; ERR519516     1  0.2948     0.5756 0.804 0.008 0.000 0.000 0.188 0.000
#&gt; ERR519520     2  0.6146     0.0942 0.248 0.404 0.000 0.004 0.344 0.000
#&gt; ERR519513     1  0.5058     0.4205 0.600 0.000 0.000 0.108 0.292 0.000
#&gt; ERR519481     5  0.4087     0.4977 0.120 0.012 0.000 0.096 0.772 0.000
#&gt; ERR519491     1  0.0146     0.5939 0.996 0.000 0.000 0.000 0.004 0.000
#&gt; ERR519473     5  0.5305     0.4240 0.404 0.000 0.000 0.104 0.492 0.000
#&gt; ERR519518     4  0.5400     0.5238 0.000 0.264 0.000 0.572 0.164 0.000
#&gt; ERR519512     5  0.5156     0.3599 0.188 0.156 0.000 0.008 0.648 0.000
#&gt; ERR519521     5  0.5228    -0.1062 0.000 0.400 0.000 0.096 0.504 0.000
#&gt; ERR519488     1  0.5351     0.2788 0.592 0.200 0.000 0.000 0.208 0.000
#&gt; ERR519493     1  0.0547     0.5973 0.980 0.000 0.000 0.000 0.020 0.000
#&gt; ERR519514     1  0.1267     0.6000 0.940 0.000 0.000 0.000 0.060 0.000
#&gt; ERR519479     1  0.3104     0.5619 0.788 0.004 0.000 0.004 0.204 0.000
#&gt; ERR519509     1  0.4101     0.1146 0.580 0.408 0.000 0.000 0.012 0.000
#&gt; ERR519472     1  0.3950    -0.1048 0.564 0.000 0.000 0.004 0.432 0.000
#&gt; ERR519510     1  0.2921     0.5834 0.828 0.008 0.000 0.008 0.156 0.000
#&gt; ERR519470     1  0.0458     0.5959 0.984 0.000 0.000 0.000 0.016 0.000
#&gt; ERR519495     1  0.3984     0.2305 0.596 0.008 0.000 0.000 0.396 0.000
#&gt; ERR519522     1  0.3566     0.5315 0.788 0.056 0.000 0.000 0.156 0.000
#&gt; ERR519523     1  0.3986     0.4788 0.608 0.004 0.000 0.004 0.384 0.000
#&gt; ERR519503     1  0.7315    -0.2078 0.380 0.284 0.000 0.120 0.216 0.000
#&gt; ERR519471     1  0.0865     0.5990 0.964 0.000 0.000 0.000 0.036 0.000
#&gt; ERR519500     5  0.3864    -0.0219 0.480 0.000 0.000 0.000 0.520 0.000
#&gt; ERR519485     1  0.2579     0.5648 0.872 0.040 0.000 0.000 0.088 0.000
#&gt; ERR519476     2  0.4994     0.2200 0.412 0.524 0.000 0.000 0.060 0.004
#&gt; ERR519502     5  0.4760     0.5373 0.232 0.020 0.000 0.064 0.684 0.000
#&gt; ERR519486     1  0.3695     0.5224 0.776 0.060 0.000 0.000 0.164 0.000
#&gt; ERR519478     1  0.4379     0.0971 0.576 0.396 0.000 0.000 0.028 0.000
#&gt; ERR519497     2  0.5944     0.0708 0.216 0.400 0.000 0.000 0.384 0.000
#&gt; ERR519467     1  0.1327     0.5961 0.936 0.000 0.000 0.000 0.064 0.000
#&gt; ERR519489     3  0.0000     0.9970 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519494     3  0.0000     0.9970 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519474     1  0.1806     0.5970 0.908 0.004 0.000 0.000 0.088 0.000
#&gt; ERR519505     1  0.6501     0.2558 0.468 0.080 0.000 0.108 0.344 0.000
#&gt; ERR519517     3  0.0000     0.9970 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519484     1  0.4601     0.5072 0.688 0.000 0.000 0.112 0.200 0.000
#&gt; ERR519498     1  0.5391     0.2900 0.456 0.000 0.000 0.112 0.432 0.000
#&gt; ERR519490     4  0.3890    -0.1879 0.000 0.000 0.400 0.596 0.000 0.004
#&gt; ERR519507     1  0.2902     0.5793 0.800 0.004 0.000 0.000 0.196 0.000
#&gt; ERR519511     1  0.3927     0.4956 0.644 0.012 0.000 0.000 0.344 0.000
#&gt; ERR519468     5  0.4926     0.5309 0.240 0.000 0.000 0.120 0.640 0.000
#&gt; ERR519482     4  0.5363     0.5287 0.000 0.240 0.000 0.600 0.156 0.004
#&gt; ERR519475     2  0.4994     0.2200 0.412 0.524 0.000 0.000 0.060 0.004
#&gt; ERR519496     2  0.5943     0.0338 0.380 0.404 0.000 0.000 0.216 0.000
#&gt; ERR519506     1  0.4702     0.4797 0.716 0.120 0.000 0.016 0.148 0.000
#&gt; ERR519469     5  0.5186     0.4675 0.356 0.000 0.000 0.100 0.544 0.000
#&gt; ERR519480     6  0.0000     0.0000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; ERR519487     3  0.0363     0.9878 0.000 0.000 0.988 0.012 0.000 0.000
#&gt; ERR519483     1  0.6587    -0.0436 0.480 0.292 0.000 0.060 0.168 0.000
#&gt; ERR519477     2  0.5077     0.2140 0.404 0.524 0.000 0.000 0.068 0.004
#&gt; ERR519499     3  0.0000     0.9970 0.000 0.000 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-5-a').click(function(){
  $('#tab-CV-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-CV-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-get-signatures'>
<ul>
<li><a href='#tab-CV-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-1-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-1"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-2-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-2"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-3-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-3"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-4-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-4"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-5-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-mclust-signature_compare](figure_cola/CV-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-CV-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-mclust-collect-classes](figure_cola/CV-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:NMF*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "NMF"]
# you can also extract it by
# res = res_list["CV:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 18140 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-NMF-collect-plots](figure_cola/CV-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-NMF-select-partition-number](figure_cola/CV-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.910           0.905       0.961         0.3977 0.618   0.618
#> 3 3 0.466           0.645       0.829         0.5575 0.716   0.549
#> 4 4 0.628           0.625       0.832         0.1428 0.883   0.698
#> 5 5 0.577           0.542       0.712         0.0681 0.943   0.825
#> 6 6 0.630           0.551       0.751         0.0492 0.824   0.466
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-get-classes'>
<ul>
<li><a href='#tab-CV-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-NMF-get-classes-1'>
<p><a id='tab-CV-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; ERR519515     1   0.000      0.959 1.000 0.000
#&gt; ERR519516     1   0.000      0.959 1.000 0.000
#&gt; ERR519520     1   0.000      0.959 1.000 0.000
#&gt; ERR519513     1   0.295      0.923 0.948 0.052
#&gt; ERR519481     1   0.000      0.959 1.000 0.000
#&gt; ERR519491     1   0.000      0.959 1.000 0.000
#&gt; ERR519473     1   0.000      0.959 1.000 0.000
#&gt; ERR519518     1   0.000      0.959 1.000 0.000
#&gt; ERR519512     1   0.000      0.959 1.000 0.000
#&gt; ERR519521     1   0.000      0.959 1.000 0.000
#&gt; ERR519488     1   0.000      0.959 1.000 0.000
#&gt; ERR519493     1   0.000      0.959 1.000 0.000
#&gt; ERR519514     1   0.767      0.711 0.776 0.224
#&gt; ERR519479     1   0.000      0.959 1.000 0.000
#&gt; ERR519509     1   0.000      0.959 1.000 0.000
#&gt; ERR519472     1   0.204      0.938 0.968 0.032
#&gt; ERR519510     1   0.000      0.959 1.000 0.000
#&gt; ERR519470     1   0.000      0.959 1.000 0.000
#&gt; ERR519495     2   0.775      0.694 0.228 0.772
#&gt; ERR519522     1   0.000      0.959 1.000 0.000
#&gt; ERR519523     1   0.000      0.959 1.000 0.000
#&gt; ERR519503     1   0.000      0.959 1.000 0.000
#&gt; ERR519471     1   0.000      0.959 1.000 0.000
#&gt; ERR519500     1   0.311      0.919 0.944 0.056
#&gt; ERR519485     2   0.295      0.911 0.052 0.948
#&gt; ERR519476     1   0.416      0.892 0.916 0.084
#&gt; ERR519502     1   0.000      0.959 1.000 0.000
#&gt; ERR519486     2   0.000      0.949 0.000 1.000
#&gt; ERR519478     1   0.000      0.959 1.000 0.000
#&gt; ERR519497     1   0.000      0.959 1.000 0.000
#&gt; ERR519467     1   0.000      0.959 1.000 0.000
#&gt; ERR519489     2   0.000      0.949 0.000 1.000
#&gt; ERR519494     2   0.000      0.949 0.000 1.000
#&gt; ERR519474     1   0.000      0.959 1.000 0.000
#&gt; ERR519505     1   0.000      0.959 1.000 0.000
#&gt; ERR519517     2   0.000      0.949 0.000 1.000
#&gt; ERR519484     1   0.000      0.959 1.000 0.000
#&gt; ERR519498     1   0.000      0.959 1.000 0.000
#&gt; ERR519490     2   0.000      0.949 0.000 1.000
#&gt; ERR519507     1   0.987      0.254 0.568 0.432
#&gt; ERR519511     2   0.000      0.949 0.000 1.000
#&gt; ERR519468     1   0.000      0.959 1.000 0.000
#&gt; ERR519482     2   0.871      0.600 0.292 0.708
#&gt; ERR519475     1   0.295      0.921 0.948 0.052
#&gt; ERR519496     1   0.141      0.946 0.980 0.020
#&gt; ERR519506     1   0.358      0.908 0.932 0.068
#&gt; ERR519469     1   0.000      0.959 1.000 0.000
#&gt; ERR519480     2   0.000      0.949 0.000 1.000
#&gt; ERR519487     2   0.000      0.949 0.000 1.000
#&gt; ERR519483     2   0.000      0.949 0.000 1.000
#&gt; ERR519477     1   0.994      0.149 0.544 0.456
#&gt; ERR519499     2   0.000      0.949 0.000 1.000
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-1-a').click(function(){
  $('#tab-CV-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-2'>
<p><a id='tab-CV-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; ERR519515     2  0.5016     0.6768 0.240 0.760 0.000
#&gt; ERR519516     1  0.0237     0.7921 0.996 0.004 0.000
#&gt; ERR519520     2  0.5733     0.6481 0.324 0.676 0.000
#&gt; ERR519513     1  0.2297     0.7596 0.944 0.036 0.020
#&gt; ERR519481     1  0.0424     0.7922 0.992 0.008 0.000
#&gt; ERR519491     1  0.5785     0.2331 0.668 0.332 0.000
#&gt; ERR519473     1  0.0237     0.7911 0.996 0.004 0.000
#&gt; ERR519518     1  0.6140     0.1468 0.596 0.404 0.000
#&gt; ERR519512     1  0.3038     0.7110 0.896 0.104 0.000
#&gt; ERR519521     1  0.3816     0.6418 0.852 0.148 0.000
#&gt; ERR519488     2  0.5810     0.6383 0.336 0.664 0.000
#&gt; ERR519493     1  0.0237     0.7921 0.996 0.004 0.000
#&gt; ERR519514     2  0.9872     0.4158 0.320 0.408 0.272
#&gt; ERR519479     1  0.0237     0.7921 0.996 0.004 0.000
#&gt; ERR519509     2  0.5560     0.6618 0.300 0.700 0.000
#&gt; ERR519472     1  0.0424     0.7894 0.992 0.000 0.008
#&gt; ERR519510     1  0.0424     0.7922 0.992 0.008 0.000
#&gt; ERR519470     1  0.6267    -0.2140 0.548 0.452 0.000
#&gt; ERR519495     3  0.5167     0.7024 0.192 0.016 0.792
#&gt; ERR519522     2  0.6045     0.5870 0.380 0.620 0.000
#&gt; ERR519523     2  0.6008     0.5969 0.372 0.628 0.000
#&gt; ERR519503     2  0.2066     0.6280 0.060 0.940 0.000
#&gt; ERR519471     1  0.6168    -0.0718 0.588 0.412 0.000
#&gt; ERR519500     1  0.0892     0.7832 0.980 0.000 0.020
#&gt; ERR519485     3  0.2959     0.8437 0.000 0.100 0.900
#&gt; ERR519476     2  0.6057     0.5378 0.196 0.760 0.044
#&gt; ERR519502     1  0.0424     0.7922 0.992 0.008 0.000
#&gt; ERR519486     3  0.0000     0.9288 0.000 0.000 1.000
#&gt; ERR519478     2  0.5016     0.6771 0.240 0.760 0.000
#&gt; ERR519497     1  0.6280    -0.0979 0.540 0.460 0.000
#&gt; ERR519467     2  0.6045     0.5870 0.380 0.620 0.000
#&gt; ERR519489     3  0.0000     0.9288 0.000 0.000 1.000
#&gt; ERR519494     3  0.0000     0.9288 0.000 0.000 1.000
#&gt; ERR519474     1  0.5327     0.3987 0.728 0.272 0.000
#&gt; ERR519505     1  0.2066     0.7638 0.940 0.060 0.000
#&gt; ERR519517     3  0.0000     0.9288 0.000 0.000 1.000
#&gt; ERR519484     1  0.0592     0.7919 0.988 0.012 0.000
#&gt; ERR519498     1  0.0424     0.7922 0.992 0.008 0.000
#&gt; ERR519490     3  0.0000     0.9288 0.000 0.000 1.000
#&gt; ERR519507     1  0.5733     0.3663 0.676 0.000 0.324
#&gt; ERR519511     3  0.0000     0.9288 0.000 0.000 1.000
#&gt; ERR519468     1  0.0424     0.7909 0.992 0.008 0.000
#&gt; ERR519482     2  0.8882     0.2023 0.316 0.540 0.144
#&gt; ERR519475     2  0.5585     0.5758 0.204 0.772 0.024
#&gt; ERR519496     2  0.2772     0.6387 0.080 0.916 0.004
#&gt; ERR519506     1  0.4196     0.6811 0.864 0.112 0.024
#&gt; ERR519469     1  0.0237     0.7911 0.996 0.004 0.000
#&gt; ERR519480     3  0.5656     0.7187 0.004 0.284 0.712
#&gt; ERR519487     3  0.0000     0.9288 0.000 0.000 1.000
#&gt; ERR519483     3  0.4782     0.8222 0.016 0.164 0.820
#&gt; ERR519477     2  0.9725     0.3514 0.272 0.452 0.276
#&gt; ERR519499     3  0.0000     0.9288 0.000 0.000 1.000
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-2-a').click(function(){
  $('#tab-CV-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-3'>
<p><a id='tab-CV-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; ERR519515     1  0.2021     0.6745 0.932 0.056 0.000 0.012
#&gt; ERR519516     4  0.0000     0.8327 0.000 0.000 0.000 1.000
#&gt; ERR519520     1  0.0927     0.6913 0.976 0.008 0.000 0.016
#&gt; ERR519513     4  0.2125     0.8193 0.004 0.076 0.000 0.920
#&gt; ERR519481     4  0.1209     0.8325 0.004 0.032 0.000 0.964
#&gt; ERR519491     4  0.4933     0.1640 0.432 0.000 0.000 0.568
#&gt; ERR519473     4  0.0188     0.8321 0.000 0.004 0.000 0.996
#&gt; ERR519518     4  0.7690     0.1105 0.264 0.280 0.000 0.456
#&gt; ERR519512     4  0.4744     0.5964 0.284 0.012 0.000 0.704
#&gt; ERR519521     4  0.4336     0.7265 0.128 0.060 0.000 0.812
#&gt; ERR519488     1  0.1042     0.6909 0.972 0.008 0.000 0.020
#&gt; ERR519493     4  0.0000     0.8327 0.000 0.000 0.000 1.000
#&gt; ERR519514     1  0.6937     0.2428 0.564 0.012 0.332 0.092
#&gt; ERR519479     4  0.0000     0.8327 0.000 0.000 0.000 1.000
#&gt; ERR519509     1  0.0188     0.6864 0.996 0.000 0.000 0.004
#&gt; ERR519472     4  0.0564     0.8309 0.004 0.004 0.004 0.988
#&gt; ERR519510     4  0.1824     0.8255 0.004 0.060 0.000 0.936
#&gt; ERR519470     1  0.4567     0.5138 0.740 0.016 0.000 0.244
#&gt; ERR519495     3  0.4908     0.4018 0.000 0.016 0.692 0.292
#&gt; ERR519522     1  0.1706     0.6887 0.948 0.016 0.000 0.036
#&gt; ERR519523     1  0.2179     0.6831 0.924 0.012 0.000 0.064
#&gt; ERR519503     1  0.3356     0.5749 0.824 0.176 0.000 0.000
#&gt; ERR519471     1  0.5289     0.4013 0.636 0.020 0.000 0.344
#&gt; ERR519500     4  0.2990     0.7951 0.036 0.008 0.056 0.900
#&gt; ERR519485     3  0.2781     0.8324 0.012 0.036 0.912 0.040
#&gt; ERR519476     2  0.5977     0.1216 0.388 0.572 0.004 0.036
#&gt; ERR519502     4  0.1022     0.8328 0.000 0.032 0.000 0.968
#&gt; ERR519486     3  0.0000     0.9269 0.000 0.000 1.000 0.000
#&gt; ERR519478     1  0.1489     0.6752 0.952 0.044 0.000 0.004
#&gt; ERR519497     1  0.7651     0.0430 0.464 0.248 0.000 0.288
#&gt; ERR519467     1  0.1584     0.6898 0.952 0.012 0.000 0.036
#&gt; ERR519489     3  0.0000     0.9269 0.000 0.000 1.000 0.000
#&gt; ERR519494     3  0.0000     0.9269 0.000 0.000 1.000 0.000
#&gt; ERR519474     4  0.5112     0.3135 0.384 0.008 0.000 0.608
#&gt; ERR519505     4  0.4292     0.7705 0.080 0.100 0.000 0.820
#&gt; ERR519517     3  0.0000     0.9269 0.000 0.000 1.000 0.000
#&gt; ERR519484     4  0.1489     0.8302 0.004 0.044 0.000 0.952
#&gt; ERR519498     4  0.2266     0.8159 0.004 0.084 0.000 0.912
#&gt; ERR519490     3  0.0000     0.9269 0.000 0.000 1.000 0.000
#&gt; ERR519507     4  0.4086     0.6323 0.000 0.008 0.216 0.776
#&gt; ERR519511     3  0.0000     0.9269 0.000 0.000 1.000 0.000
#&gt; ERR519468     4  0.1118     0.8332 0.000 0.036 0.000 0.964
#&gt; ERR519482     2  0.5937     0.3845 0.216 0.708 0.032 0.044
#&gt; ERR519475     1  0.6370     0.0884 0.556 0.392 0.024 0.028
#&gt; ERR519496     1  0.3569     0.5583 0.804 0.196 0.000 0.000
#&gt; ERR519506     4  0.6863     0.4967 0.220 0.120 0.020 0.640
#&gt; ERR519469     4  0.0188     0.8321 0.000 0.004 0.000 0.996
#&gt; ERR519480     2  0.4800     0.3074 0.004 0.656 0.340 0.000
#&gt; ERR519487     3  0.0000     0.9269 0.000 0.000 1.000 0.000
#&gt; ERR519483     2  0.6552    -0.0405 0.024 0.476 0.468 0.032
#&gt; ERR519477     1  0.9921    -0.1916 0.292 0.260 0.192 0.256
#&gt; ERR519499     3  0.0000     0.9269 0.000 0.000 1.000 0.000
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-3-a').click(function(){
  $('#tab-CV-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-4'>
<p><a id='tab-CV-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; ERR519515     1  0.2624     0.5755 0.872 0.116 0.000 0.012 0.000
#&gt; ERR519516     4  0.1894     0.6811 0.008 0.072 0.000 0.920 0.000
#&gt; ERR519520     1  0.1041     0.6192 0.964 0.032 0.000 0.004 0.000
#&gt; ERR519513     4  0.4283     0.5878 0.000 0.348 0.000 0.644 0.008
#&gt; ERR519481     4  0.3612     0.6415 0.000 0.228 0.000 0.764 0.008
#&gt; ERR519491     4  0.4557     0.1649 0.404 0.000 0.000 0.584 0.012
#&gt; ERR519473     4  0.0162     0.6700 0.000 0.000 0.000 0.996 0.004
#&gt; ERR519518     2  0.5538     0.5729 0.148 0.680 0.000 0.160 0.012
#&gt; ERR519512     4  0.6347     0.2417 0.408 0.160 0.000 0.432 0.000
#&gt; ERR519521     4  0.5368     0.5261 0.068 0.308 0.000 0.620 0.004
#&gt; ERR519488     1  0.0451     0.6270 0.988 0.000 0.000 0.008 0.004
#&gt; ERR519493     4  0.2230     0.6780 0.000 0.116 0.000 0.884 0.000
#&gt; ERR519514     1  0.6768     0.2178 0.492 0.000 0.308 0.184 0.016
#&gt; ERR519479     4  0.0404     0.6735 0.000 0.012 0.000 0.988 0.000
#&gt; ERR519509     1  0.0451     0.6249 0.988 0.008 0.000 0.004 0.000
#&gt; ERR519472     4  0.0968     0.6650 0.004 0.000 0.012 0.972 0.012
#&gt; ERR519510     4  0.4403     0.5916 0.008 0.340 0.000 0.648 0.004
#&gt; ERR519470     1  0.4305     0.5117 0.748 0.000 0.000 0.200 0.052
#&gt; ERR519495     4  0.4593    -0.1012 0.004 0.000 0.480 0.512 0.004
#&gt; ERR519522     1  0.1485     0.6253 0.948 0.000 0.000 0.032 0.020
#&gt; ERR519523     1  0.2915     0.5942 0.860 0.024 0.000 0.116 0.000
#&gt; ERR519503     1  0.4547     0.0280 0.588 0.400 0.000 0.000 0.012
#&gt; ERR519471     1  0.5084     0.3910 0.616 0.000 0.000 0.332 0.052
#&gt; ERR519500     4  0.3696     0.6022 0.092 0.000 0.040 0.840 0.028
#&gt; ERR519485     3  0.3270     0.7547 0.004 0.000 0.852 0.100 0.044
#&gt; ERR519476     2  0.6806     0.4022 0.252 0.500 0.008 0.004 0.236
#&gt; ERR519502     4  0.3992     0.6230 0.004 0.280 0.000 0.712 0.004
#&gt; ERR519486     3  0.0000     0.9682 0.000 0.000 1.000 0.000 0.000
#&gt; ERR519478     1  0.2179     0.5745 0.888 0.112 0.000 0.000 0.000
#&gt; ERR519497     2  0.5150     0.6134 0.272 0.652 0.000 0.076 0.000
#&gt; ERR519467     1  0.1267     0.6265 0.960 0.004 0.000 0.024 0.012
#&gt; ERR519489     3  0.0000     0.9682 0.000 0.000 1.000 0.000 0.000
#&gt; ERR519494     3  0.0162     0.9686 0.000 0.000 0.996 0.000 0.004
#&gt; ERR519474     4  0.4134     0.4736 0.264 0.008 0.000 0.720 0.008
#&gt; ERR519505     4  0.6342     0.3577 0.112 0.420 0.000 0.456 0.012
#&gt; ERR519517     3  0.0000     0.9682 0.000 0.000 1.000 0.000 0.000
#&gt; ERR519484     4  0.4183     0.6035 0.000 0.324 0.000 0.668 0.008
#&gt; ERR519498     4  0.4341     0.5734 0.000 0.364 0.000 0.628 0.008
#&gt; ERR519490     3  0.0162     0.9686 0.000 0.000 0.996 0.000 0.004
#&gt; ERR519507     4  0.3209     0.5539 0.000 0.000 0.180 0.812 0.008
#&gt; ERR519511     3  0.0290     0.9605 0.000 0.008 0.992 0.000 0.000
#&gt; ERR519468     4  0.2389     0.6748 0.000 0.116 0.000 0.880 0.004
#&gt; ERR519482     2  0.5532     0.5365 0.124 0.708 0.000 0.036 0.132
#&gt; ERR519475     1  0.7111    -0.3886 0.420 0.416 0.020 0.020 0.124
#&gt; ERR519496     1  0.5221    -0.0576 0.552 0.400 0.000 0.000 0.048
#&gt; ERR519506     4  0.7253     0.0764 0.176 0.028 0.012 0.492 0.292
#&gt; ERR519469     4  0.0162     0.6700 0.000 0.000 0.000 0.996 0.004
#&gt; ERR519480     5  0.6389     0.5280 0.008 0.232 0.204 0.000 0.556
#&gt; ERR519487     3  0.0162     0.9686 0.000 0.000 0.996 0.000 0.004
#&gt; ERR519483     5  0.5210     0.5142 0.016 0.064 0.144 0.028 0.748
#&gt; ERR519477     1  0.9989    -0.2976 0.216 0.184 0.192 0.196 0.212
#&gt; ERR519499     3  0.0162     0.9686 0.000 0.000 0.996 0.000 0.004
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-4-a').click(function(){
  $('#tab-CV-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-5'>
<p><a id='tab-CV-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; ERR519515     1  0.2730     0.5868 0.808 0.192 0.000 0.000 0.000 0.000
#&gt; ERR519516     5  0.3121     0.2712 0.008 0.004 0.000 0.192 0.796 0.000
#&gt; ERR519520     1  0.0820     0.7301 0.972 0.012 0.000 0.016 0.000 0.000
#&gt; ERR519513     4  0.3584     0.8612 0.000 0.004 0.000 0.688 0.308 0.000
#&gt; ERR519481     5  0.3975    -0.5879 0.000 0.004 0.000 0.452 0.544 0.000
#&gt; ERR519491     5  0.3890     0.2816 0.400 0.000 0.000 0.004 0.596 0.000
#&gt; ERR519473     5  0.0405     0.5777 0.000 0.000 0.000 0.004 0.988 0.008
#&gt; ERR519518     2  0.5505     0.4852 0.068 0.648 0.000 0.208 0.076 0.000
#&gt; ERR519512     1  0.5519     0.0767 0.520 0.000 0.000 0.332 0.148 0.000
#&gt; ERR519521     4  0.5240     0.6147 0.016 0.056 0.000 0.488 0.440 0.000
#&gt; ERR519488     1  0.0000     0.7327 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; ERR519493     5  0.3448     0.1193 0.000 0.004 0.000 0.280 0.716 0.000
#&gt; ERR519514     5  0.6205     0.0433 0.356 0.000 0.272 0.004 0.368 0.000
#&gt; ERR519479     5  0.1080     0.5601 0.004 0.004 0.000 0.032 0.960 0.000
#&gt; ERR519509     1  0.0547     0.7297 0.980 0.020 0.000 0.000 0.000 0.000
#&gt; ERR519472     5  0.1003     0.5876 0.004 0.000 0.028 0.000 0.964 0.004
#&gt; ERR519510     4  0.3371     0.8610 0.000 0.000 0.000 0.708 0.292 0.000
#&gt; ERR519470     1  0.2994     0.6036 0.788 0.000 0.000 0.004 0.208 0.000
#&gt; ERR519495     5  0.3606     0.4673 0.000 0.004 0.264 0.000 0.724 0.008
#&gt; ERR519522     1  0.0806     0.7320 0.972 0.000 0.000 0.008 0.020 0.000
#&gt; ERR519523     1  0.3017     0.6825 0.840 0.052 0.000 0.000 0.108 0.000
#&gt; ERR519503     2  0.3717     0.4258 0.384 0.616 0.000 0.000 0.000 0.000
#&gt; ERR519471     5  0.4635     0.0334 0.476 0.000 0.000 0.024 0.492 0.008
#&gt; ERR519500     5  0.4009     0.5803 0.128 0.004 0.040 0.036 0.792 0.000
#&gt; ERR519485     3  0.2201     0.8763 0.004 0.016 0.912 0.004 0.056 0.008
#&gt; ERR519476     2  0.5889     0.4156 0.180 0.640 0.008 0.120 0.004 0.048
#&gt; ERR519502     4  0.3930     0.7692 0.000 0.004 0.000 0.576 0.420 0.000
#&gt; ERR519486     3  0.0000     0.9846 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519478     1  0.2300     0.6428 0.856 0.144 0.000 0.000 0.000 0.000
#&gt; ERR519497     2  0.5344     0.4427 0.120 0.532 0.000 0.348 0.000 0.000
#&gt; ERR519467     1  0.1307     0.7273 0.952 0.008 0.000 0.032 0.008 0.000
#&gt; ERR519489     3  0.0000     0.9846 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519494     3  0.0000     0.9846 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519474     5  0.4107     0.5120 0.280 0.004 0.000 0.028 0.688 0.000
#&gt; ERR519505     4  0.4715     0.7466 0.080 0.024 0.000 0.712 0.184 0.000
#&gt; ERR519517     3  0.0000     0.9846 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519484     4  0.3592     0.8457 0.000 0.000 0.000 0.656 0.344 0.000
#&gt; ERR519498     4  0.3595     0.8559 0.000 0.008 0.000 0.704 0.288 0.000
#&gt; ERR519490     3  0.0000     0.9846 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519507     5  0.2737     0.5434 0.000 0.000 0.160 0.004 0.832 0.004
#&gt; ERR519511     3  0.0146     0.9800 0.000 0.000 0.996 0.004 0.000 0.000
#&gt; ERR519468     5  0.1268     0.5609 0.000 0.004 0.000 0.036 0.952 0.008
#&gt; ERR519482     2  0.4970     0.4968 0.068 0.744 0.000 0.080 0.016 0.092
#&gt; ERR519475     2  0.5954     0.5187 0.264 0.612 0.020 0.060 0.020 0.024
#&gt; ERR519496     2  0.3464     0.5187 0.312 0.688 0.000 0.000 0.000 0.000
#&gt; ERR519506     5  0.6995     0.3397 0.132 0.108 0.000 0.200 0.536 0.024
#&gt; ERR519469     5  0.0665     0.5786 0.000 0.008 0.000 0.004 0.980 0.008
#&gt; ERR519480     6  0.2488     0.0000 0.000 0.044 0.076 0.000 0.000 0.880
#&gt; ERR519487     3  0.0000     0.9846 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519483     2  0.7680    -0.4319 0.012 0.308 0.092 0.284 0.004 0.300
#&gt; ERR519477     1  0.9858    -0.2581 0.244 0.168 0.152 0.128 0.132 0.176
#&gt; ERR519499     3  0.0000     0.9846 0.000 0.000 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-5-a').click(function(){
  $('#tab-CV-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-CV-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-get-signatures'>
<ul>
<li><a href='#tab-CV-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-1-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-1"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-2-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-2"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-3-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-3"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-4-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-4"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-5-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-NMF-signature_compare](figure_cola/CV-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-CV-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-NMF-collect-classes](figure_cola/CV-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:hclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "hclust"]
# you can also extract it by
# res = res_list["MAD:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 18140 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-hclust-collect-plots](figure_cola/MAD-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-hclust-select-partition-number](figure_cola/MAD-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000          0.112 0.889   0.889
#> 3 3 0.429           0.609       0.768          3.273 0.729   0.695
#> 4 4 0.420           0.652       0.749          0.349 0.686   0.498
#> 5 5 0.611           0.626       0.782          0.180 0.843   0.548
#> 6 6 0.660           0.682       0.762          0.029 0.975   0.887
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-get-classes'>
<ul>
<li><a href='#tab-MAD-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-hclust-get-classes-1'>
<p><a id='tab-MAD-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette p1 p2
#&gt; ERR519515     1       0          1  1  0
#&gt; ERR519516     1       0          1  1  0
#&gt; ERR519520     1       0          1  1  0
#&gt; ERR519513     1       0          1  1  0
#&gt; ERR519481     1       0          1  1  0
#&gt; ERR519491     1       0          1  1  0
#&gt; ERR519473     1       0          1  1  0
#&gt; ERR519518     1       0          1  1  0
#&gt; ERR519512     1       0          1  1  0
#&gt; ERR519521     1       0          1  1  0
#&gt; ERR519488     1       0          1  1  0
#&gt; ERR519493     1       0          1  1  0
#&gt; ERR519514     1       0          1  1  0
#&gt; ERR519479     1       0          1  1  0
#&gt; ERR519509     1       0          1  1  0
#&gt; ERR519472     1       0          1  1  0
#&gt; ERR519510     1       0          1  1  0
#&gt; ERR519470     1       0          1  1  0
#&gt; ERR519495     1       0          1  1  0
#&gt; ERR519522     1       0          1  1  0
#&gt; ERR519523     1       0          1  1  0
#&gt; ERR519503     1       0          1  1  0
#&gt; ERR519471     1       0          1  1  0
#&gt; ERR519500     1       0          1  1  0
#&gt; ERR519485     1       0          1  1  0
#&gt; ERR519476     2       0          1  0  1
#&gt; ERR519502     1       0          1  1  0
#&gt; ERR519486     1       0          1  1  0
#&gt; ERR519478     1       0          1  1  0
#&gt; ERR519497     1       0          1  1  0
#&gt; ERR519467     1       0          1  1  0
#&gt; ERR519489     1       0          1  1  0
#&gt; ERR519494     1       0          1  1  0
#&gt; ERR519474     1       0          1  1  0
#&gt; ERR519505     1       0          1  1  0
#&gt; ERR519517     1       0          1  1  0
#&gt; ERR519484     1       0          1  1  0
#&gt; ERR519498     1       0          1  1  0
#&gt; ERR519490     1       0          1  1  0
#&gt; ERR519507     1       0          1  1  0
#&gt; ERR519511     1       0          1  1  0
#&gt; ERR519468     1       0          1  1  0
#&gt; ERR519482     1       0          1  1  0
#&gt; ERR519475     2       0          1  0  1
#&gt; ERR519496     1       0          1  1  0
#&gt; ERR519506     1       0          1  1  0
#&gt; ERR519469     1       0          1  1  0
#&gt; ERR519480     1       0          1  1  0
#&gt; ERR519487     1       0          1  1  0
#&gt; ERR519483     1       0          1  1  0
#&gt; ERR519477     2       0          1  0  1
#&gt; ERR519499     1       0          1  1  0
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-1-a').click(function(){
  $('#tab-MAD-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-2'>
<p><a id='tab-MAD-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3
#&gt; ERR519515     1  0.5678      0.637 0.684  0 0.316
#&gt; ERR519516     1  0.5098      0.651 0.752  0 0.248
#&gt; ERR519520     1  0.5650      0.643 0.688  0 0.312
#&gt; ERR519513     1  0.4974      0.360 0.764  0 0.236
#&gt; ERR519481     1  0.5650      0.180 0.688  0 0.312
#&gt; ERR519491     1  0.5098      0.651 0.752  0 0.248
#&gt; ERR519473     1  0.5650      0.180 0.688  0 0.312
#&gt; ERR519518     1  0.6225     -0.333 0.568  0 0.432
#&gt; ERR519512     1  0.5650      0.643 0.688  0 0.312
#&gt; ERR519521     1  0.5650      0.180 0.688  0 0.312
#&gt; ERR519488     1  0.5678      0.637 0.684  0 0.316
#&gt; ERR519493     1  0.5098      0.651 0.752  0 0.248
#&gt; ERR519514     1  0.5678      0.637 0.684  0 0.316
#&gt; ERR519479     1  0.2261      0.585 0.932  0 0.068
#&gt; ERR519509     1  0.5678      0.637 0.684  0 0.316
#&gt; ERR519472     1  0.5650      0.180 0.688  0 0.312
#&gt; ERR519510     1  0.2448      0.637 0.924  0 0.076
#&gt; ERR519470     1  0.5678      0.637 0.684  0 0.316
#&gt; ERR519495     1  0.1289      0.616 0.968  0 0.032
#&gt; ERR519522     1  0.5678      0.637 0.684  0 0.316
#&gt; ERR519523     1  0.5650      0.643 0.688  0 0.312
#&gt; ERR519503     1  0.5678      0.637 0.684  0 0.316
#&gt; ERR519471     1  0.5678      0.637 0.684  0 0.316
#&gt; ERR519500     1  0.5560      0.260 0.700  0 0.300
#&gt; ERR519485     1  0.0592      0.627 0.988  0 0.012
#&gt; ERR519476     2  0.0000      1.000 0.000  1 0.000
#&gt; ERR519502     1  0.5650      0.180 0.688  0 0.312
#&gt; ERR519486     1  0.0592      0.627 0.988  0 0.012
#&gt; ERR519478     1  0.5678      0.637 0.684  0 0.316
#&gt; ERR519497     1  0.5678      0.125 0.684  0 0.316
#&gt; ERR519467     1  0.5591      0.641 0.696  0 0.304
#&gt; ERR519489     1  0.5465      0.290 0.712  0 0.288
#&gt; ERR519494     3  0.5678      0.995 0.316  0 0.684
#&gt; ERR519474     1  0.1411      0.610 0.964  0 0.036
#&gt; ERR519505     1  0.4931      0.367 0.768  0 0.232
#&gt; ERR519517     3  0.5678      0.995 0.316  0 0.684
#&gt; ERR519484     1  0.2537      0.575 0.920  0 0.080
#&gt; ERR519498     1  0.4931      0.367 0.768  0 0.232
#&gt; ERR519490     3  0.5678      0.995 0.316  0 0.684
#&gt; ERR519507     1  0.2261      0.585 0.932  0 0.068
#&gt; ERR519511     1  0.2448      0.637 0.924  0 0.076
#&gt; ERR519468     3  0.5760      0.981 0.328  0 0.672
#&gt; ERR519482     3  0.5678      0.995 0.316  0 0.684
#&gt; ERR519475     2  0.0000      1.000 0.000  1 0.000
#&gt; ERR519496     1  0.1289      0.616 0.968  0 0.032
#&gt; ERR519506     1  0.3686      0.509 0.860  0 0.140
#&gt; ERR519469     3  0.5760      0.981 0.328  0 0.672
#&gt; ERR519480     3  0.5678      0.995 0.316  0 0.684
#&gt; ERR519487     3  0.5678      0.995 0.316  0 0.684
#&gt; ERR519483     1  0.3116      0.550 0.892  0 0.108
#&gt; ERR519477     2  0.0000      1.000 0.000  1 0.000
#&gt; ERR519499     3  0.5678      0.995 0.316  0 0.684
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-2-a').click(function(){
  $('#tab-MAD-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-3'>
<p><a id='tab-MAD-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3    p4
#&gt; ERR519515     1  0.0000      0.882 1.000  0 0.000 0.000
#&gt; ERR519516     1  0.4194      0.652 0.764  0 0.008 0.228
#&gt; ERR519520     1  0.3900      0.756 0.816  0 0.020 0.164
#&gt; ERR519513     4  0.4237      0.574 0.152  0 0.040 0.808
#&gt; ERR519481     4  0.5523      0.376 0.024  0 0.380 0.596
#&gt; ERR519491     1  0.4194      0.652 0.764  0 0.008 0.228
#&gt; ERR519473     4  0.5482      0.391 0.024  0 0.368 0.608
#&gt; ERR519518     3  0.4989     -0.132 0.000  0 0.528 0.472
#&gt; ERR519512     1  0.3900      0.756 0.816  0 0.020 0.164
#&gt; ERR519521     4  0.5523      0.376 0.024  0 0.380 0.596
#&gt; ERR519488     1  0.0000      0.882 1.000  0 0.000 0.000
#&gt; ERR519493     1  0.4194      0.652 0.764  0 0.008 0.228
#&gt; ERR519514     1  0.0000      0.882 1.000  0 0.000 0.000
#&gt; ERR519479     4  0.6649      0.618 0.340  0 0.100 0.560
#&gt; ERR519509     1  0.0000      0.882 1.000  0 0.000 0.000
#&gt; ERR519472     4  0.5482      0.391 0.024  0 0.368 0.608
#&gt; ERR519510     4  0.5236      0.493 0.432  0 0.008 0.560
#&gt; ERR519470     1  0.0000      0.882 1.000  0 0.000 0.000
#&gt; ERR519495     4  0.6179      0.568 0.392  0 0.056 0.552
#&gt; ERR519522     1  0.0000      0.882 1.000  0 0.000 0.000
#&gt; ERR519523     1  0.3900      0.756 0.816  0 0.020 0.164
#&gt; ERR519503     1  0.0000      0.882 1.000  0 0.000 0.000
#&gt; ERR519471     1  0.0000      0.882 1.000  0 0.000 0.000
#&gt; ERR519500     4  0.6121      0.416 0.060  0 0.352 0.588
#&gt; ERR519485     4  0.4933      0.491 0.432  0 0.000 0.568
#&gt; ERR519476     2  0.0000      1.000 0.000  1 0.000 0.000
#&gt; ERR519502     4  0.5523      0.376 0.024  0 0.380 0.596
#&gt; ERR519486     4  0.4933      0.491 0.432  0 0.000 0.568
#&gt; ERR519478     1  0.0000      0.882 1.000  0 0.000 0.000
#&gt; ERR519497     4  0.6499      0.423 0.112  0 0.276 0.612
#&gt; ERR519467     1  0.0524      0.877 0.988  0 0.004 0.008
#&gt; ERR519489     4  0.6265      0.436 0.072  0 0.340 0.588
#&gt; ERR519494     3  0.3123      0.680 0.000  0 0.844 0.156
#&gt; ERR519474     4  0.5404      0.617 0.328  0 0.028 0.644
#&gt; ERR519505     4  0.3695      0.593 0.156  0 0.016 0.828
#&gt; ERR519517     3  0.0469      0.783 0.000  0 0.988 0.012
#&gt; ERR519484     4  0.5636      0.598 0.308  0 0.044 0.648
#&gt; ERR519498     4  0.3910      0.595 0.156  0 0.024 0.820
#&gt; ERR519490     3  0.0336      0.777 0.000  0 0.992 0.008
#&gt; ERR519507     4  0.6649      0.618 0.340  0 0.100 0.560
#&gt; ERR519511     4  0.5236      0.493 0.432  0 0.008 0.560
#&gt; ERR519468     3  0.3610      0.661 0.000  0 0.800 0.200
#&gt; ERR519482     3  0.0336      0.777 0.000  0 0.992 0.008
#&gt; ERR519475     2  0.0000      1.000 0.000  1 0.000 0.000
#&gt; ERR519496     4  0.6179      0.568 0.392  0 0.056 0.552
#&gt; ERR519506     4  0.5716      0.621 0.272  0 0.060 0.668
#&gt; ERR519469     3  0.3610      0.661 0.000  0 0.800 0.200
#&gt; ERR519480     3  0.4804      0.369 0.000  0 0.616 0.384
#&gt; ERR519487     3  0.0469      0.783 0.000  0 0.988 0.012
#&gt; ERR519483     4  0.5411      0.593 0.312  0 0.032 0.656
#&gt; ERR519477     2  0.0000      1.000 0.000  1 0.000 0.000
#&gt; ERR519499     3  0.0469      0.783 0.000  0 0.988 0.012
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-3-a').click(function(){
  $('#tab-MAD-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-4'>
<p><a id='tab-MAD-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3    p4    p5
#&gt; ERR519515     1  0.0000     0.9310 1.000  0 0.000 0.000 0.000
#&gt; ERR519516     5  0.4968     0.3213 0.456  0 0.000 0.028 0.516
#&gt; ERR519520     1  0.3979     0.7522 0.780  0 0.016 0.188 0.016
#&gt; ERR519513     4  0.5178    -0.2077 0.000  0 0.040 0.480 0.480
#&gt; ERR519481     4  0.4341     0.5671 0.000  0 0.364 0.628 0.008
#&gt; ERR519491     5  0.4968     0.3213 0.456  0 0.000 0.028 0.516
#&gt; ERR519473     4  0.5687     0.5375 0.000  0 0.316 0.580 0.104
#&gt; ERR519518     3  0.5148    -0.3289 0.000  0 0.528 0.432 0.040
#&gt; ERR519512     1  0.3979     0.7522 0.780  0 0.016 0.188 0.016
#&gt; ERR519521     4  0.4341     0.5671 0.000  0 0.364 0.628 0.008
#&gt; ERR519488     1  0.0000     0.9310 1.000  0 0.000 0.000 0.000
#&gt; ERR519493     5  0.4968     0.3213 0.456  0 0.000 0.028 0.516
#&gt; ERR519514     1  0.0000     0.9310 1.000  0 0.000 0.000 0.000
#&gt; ERR519479     5  0.4138     0.6601 0.028  0 0.056 0.104 0.812
#&gt; ERR519509     1  0.0000     0.9310 1.000  0 0.000 0.000 0.000
#&gt; ERR519472     4  0.5687     0.5375 0.000  0 0.316 0.580 0.104
#&gt; ERR519510     5  0.4269     0.6948 0.116  0 0.000 0.108 0.776
#&gt; ERR519470     1  0.0000     0.9310 1.000  0 0.000 0.000 0.000
#&gt; ERR519495     5  0.4711     0.6894 0.080  0 0.044 0.096 0.780
#&gt; ERR519522     1  0.0000     0.9310 1.000  0 0.000 0.000 0.000
#&gt; ERR519523     1  0.3979     0.7522 0.780  0 0.016 0.188 0.016
#&gt; ERR519503     1  0.0000     0.9310 1.000  0 0.000 0.000 0.000
#&gt; ERR519471     1  0.0000     0.9310 1.000  0 0.000 0.000 0.000
#&gt; ERR519500     4  0.5240     0.5713 0.028  0 0.336 0.616 0.020
#&gt; ERR519485     5  0.2074     0.7051 0.104  0 0.000 0.000 0.896
#&gt; ERR519476     2  0.0000     1.0000 0.000  1 0.000 0.000 0.000
#&gt; ERR519502     4  0.4341     0.5671 0.000  0 0.364 0.628 0.008
#&gt; ERR519486     5  0.2074     0.7051 0.104  0 0.000 0.000 0.896
#&gt; ERR519478     1  0.0000     0.9310 1.000  0 0.000 0.000 0.000
#&gt; ERR519497     4  0.6155     0.3141 0.000  0 0.276 0.548 0.176
#&gt; ERR519467     1  0.0807     0.9160 0.976  0 0.000 0.012 0.012
#&gt; ERR519489     4  0.5430     0.5742 0.028  0 0.324 0.616 0.032
#&gt; ERR519494     3  0.3106     0.6392 0.000  0 0.844 0.132 0.024
#&gt; ERR519474     5  0.5453     0.2312 0.044  0 0.008 0.420 0.528
#&gt; ERR519505     4  0.4562    -0.2030 0.000  0 0.008 0.500 0.492
#&gt; ERR519517     3  0.0404     0.7507 0.000  0 0.988 0.012 0.000
#&gt; ERR519484     5  0.4264     0.5945 0.000  0 0.044 0.212 0.744
#&gt; ERR519498     5  0.4748     0.0492 0.000  0 0.016 0.492 0.492
#&gt; ERR519490     3  0.0290     0.7491 0.000  0 0.992 0.008 0.000
#&gt; ERR519507     5  0.4138     0.6601 0.028  0 0.056 0.104 0.812
#&gt; ERR519511     5  0.4269     0.6948 0.116  0 0.000 0.108 0.776
#&gt; ERR519468     3  0.4521     0.5600 0.000  0 0.748 0.164 0.088
#&gt; ERR519482     3  0.0290     0.7491 0.000  0 0.992 0.008 0.000
#&gt; ERR519475     2  0.0000     1.0000 0.000  1 0.000 0.000 0.000
#&gt; ERR519496     5  0.4711     0.6894 0.080  0 0.044 0.096 0.780
#&gt; ERR519506     5  0.2069     0.6351 0.000  0 0.012 0.076 0.912
#&gt; ERR519469     3  0.4521     0.5600 0.000  0 0.748 0.164 0.088
#&gt; ERR519480     3  0.4551     0.3810 0.000  0 0.616 0.368 0.016
#&gt; ERR519487     3  0.0404     0.7507 0.000  0 0.988 0.012 0.000
#&gt; ERR519483     5  0.2977     0.6583 0.040  0 0.008 0.076 0.876
#&gt; ERR519477     2  0.0000     1.0000 0.000  1 0.000 0.000 0.000
#&gt; ERR519499     3  0.0404     0.7507 0.000  0 0.988 0.012 0.000
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-4-a').click(function(){
  $('#tab-MAD-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-5'>
<p><a id='tab-MAD-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3    p4    p5    p6
#&gt; ERR519515     1  0.0363      0.925 0.988  0 0.000 0.000 0.012 0.000
#&gt; ERR519516     5  0.4517      0.370 0.444  0 0.000 0.032 0.524 0.000
#&gt; ERR519520     1  0.3877      0.755 0.768  0 0.016 0.188 0.024 0.004
#&gt; ERR519513     6  0.4450      0.840 0.000  0 0.032 0.108 0.104 0.756
#&gt; ERR519481     4  0.3647      0.822 0.000  0 0.360 0.640 0.000 0.000
#&gt; ERR519491     5  0.4517      0.370 0.444  0 0.000 0.032 0.524 0.000
#&gt; ERR519473     4  0.5012      0.766 0.000  0 0.300 0.600 0.100 0.000
#&gt; ERR519518     3  0.4819     -0.504 0.000  0 0.528 0.416 0.000 0.056
#&gt; ERR519512     1  0.3877      0.755 0.768  0 0.016 0.188 0.024 0.004
#&gt; ERR519521     4  0.3647      0.822 0.000  0 0.360 0.640 0.000 0.000
#&gt; ERR519488     1  0.0000      0.924 1.000  0 0.000 0.000 0.000 0.000
#&gt; ERR519493     5  0.4517      0.370 0.444  0 0.000 0.032 0.524 0.000
#&gt; ERR519514     1  0.0363      0.925 0.988  0 0.000 0.000 0.012 0.000
#&gt; ERR519479     5  0.3641      0.620 0.028  0 0.040 0.120 0.812 0.000
#&gt; ERR519509     1  0.0000      0.924 1.000  0 0.000 0.000 0.000 0.000
#&gt; ERR519472     4  0.5012      0.766 0.000  0 0.300 0.600 0.100 0.000
#&gt; ERR519510     5  0.6332      0.461 0.104  0 0.000 0.100 0.556 0.240
#&gt; ERR519470     1  0.0363      0.925 0.988  0 0.000 0.000 0.012 0.000
#&gt; ERR519495     5  0.3987      0.644 0.068  0 0.036 0.100 0.796 0.000
#&gt; ERR519522     1  0.0000      0.924 1.000  0 0.000 0.000 0.000 0.000
#&gt; ERR519523     1  0.3877      0.755 0.768  0 0.016 0.188 0.024 0.004
#&gt; ERR519503     1  0.0000      0.924 1.000  0 0.000 0.000 0.000 0.000
#&gt; ERR519471     1  0.0363      0.925 0.988  0 0.000 0.000 0.012 0.000
#&gt; ERR519500     4  0.4547      0.814 0.020  0 0.332 0.628 0.020 0.000
#&gt; ERR519485     5  0.1714      0.631 0.092  0 0.000 0.000 0.908 0.000
#&gt; ERR519476     2  0.0000      1.000 0.000  1 0.000 0.000 0.000 0.000
#&gt; ERR519502     4  0.3647      0.822 0.000  0 0.360 0.640 0.000 0.000
#&gt; ERR519486     5  0.1714      0.631 0.092  0 0.000 0.000 0.908 0.000
#&gt; ERR519478     1  0.0000      0.924 1.000  0 0.000 0.000 0.000 0.000
#&gt; ERR519497     4  0.7250      0.277 0.000  0 0.276 0.384 0.104 0.236
#&gt; ERR519467     1  0.0993      0.912 0.964  0 0.000 0.012 0.024 0.000
#&gt; ERR519489     4  0.4717      0.809 0.020  0 0.320 0.628 0.032 0.000
#&gt; ERR519494     3  0.3078      0.639 0.000  0 0.836 0.108 0.000 0.056
#&gt; ERR519474     5  0.4499      0.292 0.032  0 0.000 0.428 0.540 0.000
#&gt; ERR519505     6  0.2118      0.887 0.000  0 0.008 0.000 0.104 0.888
#&gt; ERR519517     3  0.0363      0.735 0.000  0 0.988 0.000 0.000 0.012
#&gt; ERR519484     5  0.6333      0.155 0.000  0 0.036 0.176 0.492 0.296
#&gt; ERR519498     6  0.3286      0.875 0.000  0 0.016 0.044 0.104 0.836
#&gt; ERR519490     3  0.0260      0.733 0.000  0 0.992 0.008 0.000 0.000
#&gt; ERR519507     5  0.3641      0.620 0.028  0 0.040 0.120 0.812 0.000
#&gt; ERR519511     5  0.6332      0.461 0.104  0 0.000 0.100 0.556 0.240
#&gt; ERR519468     3  0.4250      0.492 0.000  0 0.736 0.176 0.084 0.004
#&gt; ERR519482     3  0.0260      0.733 0.000  0 0.992 0.008 0.000 0.000
#&gt; ERR519475     2  0.0000      1.000 0.000  1 0.000 0.000 0.000 0.000
#&gt; ERR519496     5  0.3987      0.644 0.068  0 0.036 0.100 0.796 0.000
#&gt; ERR519506     5  0.2311      0.523 0.000  0 0.000 0.016 0.880 0.104
#&gt; ERR519469     3  0.4250      0.492 0.000  0 0.736 0.176 0.084 0.004
#&gt; ERR519480     3  0.4551      0.343 0.000  0 0.608 0.344 0.000 0.048
#&gt; ERR519487     3  0.0363      0.735 0.000  0 0.988 0.000 0.000 0.012
#&gt; ERR519483     5  0.2701      0.549 0.028  0 0.000 0.004 0.864 0.104
#&gt; ERR519477     2  0.0000      1.000 0.000  1 0.000 0.000 0.000 0.000
#&gt; ERR519499     3  0.0363      0.735 0.000  0 0.988 0.000 0.000 0.012
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-5-a').click(function(){
  $('#tab-MAD-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-get-signatures'>
<ul>
<li><a href='#tab-MAD-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-1-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-1"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-2-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-2"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-3-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-3"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-4-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-4"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-5-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-hclust-signature_compare](figure_cola/MAD-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-hclust-collect-classes](figure_cola/MAD-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:kmeans






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "kmeans"]
# you can also extract it by
# res = res_list["MAD:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 18140 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-kmeans-collect-plots](figure_cola/MAD-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-kmeans-select-partition-number](figure_cola/MAD-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.483           0.817       0.836         0.3745 0.502   0.502
#> 3 3 0.615           0.803       0.909         0.3684 0.642   0.457
#> 4 4 0.747           0.753       0.893         0.3384 0.677   0.410
#> 5 5 0.619           0.649       0.793         0.1117 0.863   0.597
#> 6 6 0.721           0.626       0.785         0.0587 0.915   0.661
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-get-classes'>
<ul>
<li><a href='#tab-MAD-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-kmeans-get-classes-1'>
<p><a id='tab-MAD-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; ERR519515     2   0.000     0.8133 0.000 1.000
#&gt; ERR519516     2   0.552     0.6894 0.128 0.872
#&gt; ERR519520     1   0.929     0.9352 0.656 0.344
#&gt; ERR519513     1   0.844     0.9278 0.728 0.272
#&gt; ERR519481     1   0.900     0.9444 0.684 0.316
#&gt; ERR519491     2   0.141     0.8117 0.020 0.980
#&gt; ERR519473     1   0.895     0.9442 0.688 0.312
#&gt; ERR519518     1   0.895     0.9442 0.688 0.312
#&gt; ERR519512     1   0.929     0.9352 0.656 0.344
#&gt; ERR519521     1   0.929     0.9352 0.656 0.344
#&gt; ERR519488     2   0.000     0.8133 0.000 1.000
#&gt; ERR519493     2   0.141     0.8117 0.020 0.980
#&gt; ERR519514     2   0.141     0.8117 0.020 0.980
#&gt; ERR519479     1   0.952     0.9074 0.628 0.372
#&gt; ERR519509     2   0.000     0.8133 0.000 1.000
#&gt; ERR519472     1   0.929     0.9352 0.656 0.344
#&gt; ERR519510     1   0.929     0.9309 0.656 0.344
#&gt; ERR519470     2   0.000     0.8133 0.000 1.000
#&gt; ERR519495     1   0.999     0.6975 0.520 0.480
#&gt; ERR519522     2   0.000     0.8133 0.000 1.000
#&gt; ERR519523     1   0.929     0.9352 0.656 0.344
#&gt; ERR519503     2   0.118     0.8049 0.016 0.984
#&gt; ERR519471     2   0.163     0.8094 0.024 0.976
#&gt; ERR519500     1   0.929     0.9352 0.656 0.344
#&gt; ERR519485     2   0.141     0.8117 0.020 0.980
#&gt; ERR519476     2   0.925     0.5737 0.340 0.660
#&gt; ERR519502     1   0.900     0.9444 0.684 0.316
#&gt; ERR519486     2   0.584     0.6748 0.140 0.860
#&gt; ERR519478     2   0.000     0.8133 0.000 1.000
#&gt; ERR519497     1   0.900     0.9444 0.684 0.316
#&gt; ERR519467     2   0.343     0.7754 0.064 0.936
#&gt; ERR519489     1   0.929     0.9352 0.656 0.344
#&gt; ERR519494     1   0.844     0.9278 0.728 0.272
#&gt; ERR519474     2   0.909     0.1379 0.324 0.676
#&gt; ERR519505     1   0.904     0.9283 0.680 0.320
#&gt; ERR519517     1   0.844     0.9278 0.728 0.272
#&gt; ERR519484     1   0.921     0.9326 0.664 0.336
#&gt; ERR519498     1   0.895     0.9443 0.688 0.312
#&gt; ERR519490     1   0.844     0.9278 0.728 0.272
#&gt; ERR519507     1   0.929     0.9309 0.656 0.344
#&gt; ERR519511     1   0.929     0.9309 0.656 0.344
#&gt; ERR519468     1   0.844     0.9278 0.728 0.272
#&gt; ERR519482     1   0.844     0.9278 0.728 0.272
#&gt; ERR519475     2   0.925     0.5737 0.340 0.660
#&gt; ERR519496     2   0.584     0.6748 0.140 0.860
#&gt; ERR519506     2   0.946     0.0881 0.364 0.636
#&gt; ERR519469     1   0.925     0.9357 0.660 0.340
#&gt; ERR519480     1   0.844     0.9278 0.728 0.272
#&gt; ERR519487     1   0.844     0.9278 0.728 0.272
#&gt; ERR519483     2   0.900     0.2427 0.316 0.684
#&gt; ERR519477     2   0.925     0.5737 0.340 0.660
#&gt; ERR519499     1   0.844     0.9278 0.728 0.272
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-1-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-2'>
<p><a id='tab-MAD-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; ERR519515     1  0.0000      0.908 1.000 0.000 0.000
#&gt; ERR519516     1  0.0237      0.907 0.996 0.004 0.000
#&gt; ERR519520     1  0.0983      0.900 0.980 0.004 0.016
#&gt; ERR519513     3  0.0829      0.798 0.012 0.004 0.984
#&gt; ERR519481     3  0.5497      0.663 0.292 0.000 0.708
#&gt; ERR519491     1  0.0000      0.908 1.000 0.000 0.000
#&gt; ERR519473     3  0.0592      0.798 0.012 0.000 0.988
#&gt; ERR519518     3  0.0829      0.798 0.012 0.004 0.984
#&gt; ERR519512     1  0.1989      0.878 0.948 0.004 0.048
#&gt; ERR519521     3  0.5722      0.664 0.292 0.004 0.704
#&gt; ERR519488     1  0.0000      0.908 1.000 0.000 0.000
#&gt; ERR519493     1  0.0000      0.908 1.000 0.000 0.000
#&gt; ERR519514     1  0.0000      0.908 1.000 0.000 0.000
#&gt; ERR519479     1  0.5497      0.591 0.708 0.000 0.292
#&gt; ERR519509     1  0.0000      0.908 1.000 0.000 0.000
#&gt; ERR519472     1  0.4750      0.716 0.784 0.000 0.216
#&gt; ERR519510     1  0.5785      0.566 0.696 0.004 0.300
#&gt; ERR519470     1  0.0000      0.908 1.000 0.000 0.000
#&gt; ERR519495     1  0.0237      0.907 0.996 0.000 0.004
#&gt; ERR519522     1  0.0000      0.908 1.000 0.000 0.000
#&gt; ERR519523     1  0.0983      0.900 0.980 0.004 0.016
#&gt; ERR519503     1  0.0000      0.908 1.000 0.000 0.000
#&gt; ERR519471     1  0.0000      0.908 1.000 0.000 0.000
#&gt; ERR519500     1  0.4233      0.778 0.836 0.004 0.160
#&gt; ERR519485     1  0.0000      0.908 1.000 0.000 0.000
#&gt; ERR519476     2  0.0829      0.995 0.004 0.984 0.012
#&gt; ERR519502     3  0.5722      0.664 0.292 0.004 0.704
#&gt; ERR519486     1  0.0000      0.908 1.000 0.000 0.000
#&gt; ERR519478     1  0.0000      0.908 1.000 0.000 0.000
#&gt; ERR519497     3  0.5722      0.664 0.292 0.004 0.704
#&gt; ERR519467     1  0.0000      0.908 1.000 0.000 0.000
#&gt; ERR519489     1  0.4834      0.731 0.792 0.004 0.204
#&gt; ERR519494     3  0.0592      0.798 0.012 0.000 0.988
#&gt; ERR519474     1  0.0237      0.907 0.996 0.000 0.004
#&gt; ERR519505     3  0.6410      0.386 0.420 0.004 0.576
#&gt; ERR519517     3  0.0829      0.798 0.012 0.004 0.984
#&gt; ERR519484     3  0.6180      0.397 0.416 0.000 0.584
#&gt; ERR519498     3  0.5722      0.664 0.292 0.004 0.704
#&gt; ERR519490     3  0.0592      0.798 0.012 0.000 0.988
#&gt; ERR519507     1  0.5560      0.575 0.700 0.000 0.300
#&gt; ERR519511     1  0.5591      0.566 0.696 0.000 0.304
#&gt; ERR519468     3  0.0592      0.798 0.012 0.000 0.988
#&gt; ERR519482     3  0.0592      0.798 0.012 0.000 0.988
#&gt; ERR519475     2  0.0237      0.998 0.004 0.996 0.000
#&gt; ERR519496     1  0.0237      0.907 0.996 0.000 0.004
#&gt; ERR519506     1  0.5016      0.676 0.760 0.000 0.240
#&gt; ERR519469     3  0.2537      0.779 0.080 0.000 0.920
#&gt; ERR519480     3  0.0592      0.798 0.012 0.000 0.988
#&gt; ERR519487     3  0.0829      0.798 0.012 0.004 0.984
#&gt; ERR519483     1  0.0237      0.907 0.996 0.000 0.004
#&gt; ERR519477     2  0.0237      0.998 0.004 0.996 0.000
#&gt; ERR519499     3  0.0829      0.798 0.012 0.004 0.984
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-2-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-3'>
<p><a id='tab-MAD-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; ERR519515     1  0.0000    0.90224 1.000 0.000 0.000 0.000
#&gt; ERR519516     1  0.4679    0.45031 0.648 0.000 0.000 0.352
#&gt; ERR519520     1  0.4955    0.06480 0.556 0.000 0.000 0.444
#&gt; ERR519513     3  0.0921    0.89123 0.000 0.000 0.972 0.028
#&gt; ERR519481     4  0.2266    0.79048 0.004 0.000 0.084 0.912
#&gt; ERR519491     1  0.1022    0.89352 0.968 0.000 0.000 0.032
#&gt; ERR519473     4  0.1452    0.81258 0.008 0.000 0.036 0.956
#&gt; ERR519518     3  0.4996    0.04247 0.000 0.000 0.516 0.484
#&gt; ERR519512     4  0.1940    0.79231 0.076 0.000 0.000 0.924
#&gt; ERR519521     4  0.1004    0.81406 0.004 0.000 0.024 0.972
#&gt; ERR519488     1  0.0336    0.90172 0.992 0.000 0.000 0.008
#&gt; ERR519493     1  0.3123    0.77463 0.844 0.000 0.000 0.156
#&gt; ERR519514     1  0.0000    0.90224 1.000 0.000 0.000 0.000
#&gt; ERR519479     4  0.1109    0.81614 0.028 0.000 0.004 0.968
#&gt; ERR519509     1  0.0336    0.90172 0.992 0.000 0.000 0.008
#&gt; ERR519472     4  0.1209    0.81574 0.032 0.000 0.004 0.964
#&gt; ERR519510     4  0.2450    0.80274 0.016 0.000 0.072 0.912
#&gt; ERR519470     1  0.0000    0.90224 1.000 0.000 0.000 0.000
#&gt; ERR519495     4  0.2647    0.77238 0.120 0.000 0.000 0.880
#&gt; ERR519522     1  0.0336    0.90172 0.992 0.000 0.000 0.008
#&gt; ERR519523     4  0.2081    0.78778 0.084 0.000 0.000 0.916
#&gt; ERR519503     1  0.1004    0.88985 0.972 0.000 0.004 0.024
#&gt; ERR519471     1  0.0188    0.90217 0.996 0.000 0.000 0.004
#&gt; ERR519500     4  0.0817    0.81557 0.024 0.000 0.000 0.976
#&gt; ERR519485     1  0.1305    0.89159 0.960 0.000 0.004 0.036
#&gt; ERR519476     2  0.0657    0.99206 0.000 0.984 0.012 0.004
#&gt; ERR519502     4  0.2125    0.79182 0.004 0.000 0.076 0.920
#&gt; ERR519486     1  0.1978    0.86769 0.928 0.000 0.004 0.068
#&gt; ERR519478     1  0.0336    0.90172 0.992 0.000 0.000 0.008
#&gt; ERR519497     4  0.3801    0.66205 0.000 0.000 0.220 0.780
#&gt; ERR519467     1  0.0469    0.90103 0.988 0.000 0.000 0.012
#&gt; ERR519489     4  0.0927    0.81648 0.016 0.000 0.008 0.976
#&gt; ERR519494     3  0.1389    0.89147 0.000 0.000 0.952 0.048
#&gt; ERR519474     4  0.5168   -0.01592 0.496 0.000 0.004 0.500
#&gt; ERR519505     4  0.4936    0.38184 0.004 0.000 0.372 0.624
#&gt; ERR519517     3  0.0817    0.89354 0.000 0.000 0.976 0.024
#&gt; ERR519484     4  0.3636    0.71425 0.008 0.000 0.172 0.820
#&gt; ERR519498     4  0.4804    0.36977 0.000 0.000 0.384 0.616
#&gt; ERR519490     3  0.2216    0.85653 0.000 0.000 0.908 0.092
#&gt; ERR519507     4  0.1388    0.81670 0.028 0.000 0.012 0.960
#&gt; ERR519511     4  0.2002    0.81120 0.020 0.000 0.044 0.936
#&gt; ERR519468     3  0.1637    0.88670 0.000 0.000 0.940 0.060
#&gt; ERR519482     3  0.1637    0.88670 0.000 0.000 0.940 0.060
#&gt; ERR519475     2  0.0000    0.99604 0.000 1.000 0.000 0.000
#&gt; ERR519496     1  0.1022    0.89352 0.968 0.000 0.000 0.032
#&gt; ERR519506     4  0.5535    0.15329 0.420 0.000 0.020 0.560
#&gt; ERR519469     4  0.1356    0.81321 0.008 0.000 0.032 0.960
#&gt; ERR519480     3  0.0592    0.89117 0.000 0.000 0.984 0.016
#&gt; ERR519487     3  0.0817    0.89354 0.000 0.000 0.976 0.024
#&gt; ERR519483     4  0.5292   -0.00894 0.480 0.000 0.008 0.512
#&gt; ERR519477     2  0.0000    0.99604 0.000 1.000 0.000 0.000
#&gt; ERR519499     3  0.0817    0.89354 0.000 0.000 0.976 0.024
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-3-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-4'>
<p><a id='tab-MAD-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; ERR519515     1  0.0290    0.80653 0.992 0.000 0.000 0.000 0.008
#&gt; ERR519516     1  0.6545    0.13709 0.464 0.000 0.000 0.316 0.220
#&gt; ERR519520     4  0.5202    0.29966 0.348 0.000 0.000 0.596 0.056
#&gt; ERR519513     5  0.4268   -0.00794 0.000 0.000 0.444 0.000 0.556
#&gt; ERR519481     4  0.3241    0.69503 0.000 0.000 0.024 0.832 0.144
#&gt; ERR519491     1  0.4367    0.65773 0.748 0.000 0.000 0.060 0.192
#&gt; ERR519473     4  0.3724    0.68963 0.000 0.000 0.028 0.788 0.184
#&gt; ERR519518     4  0.6092    0.42635 0.000 0.000 0.256 0.564 0.180
#&gt; ERR519512     4  0.1764    0.71632 0.008 0.000 0.000 0.928 0.064
#&gt; ERR519521     4  0.2338    0.69708 0.000 0.000 0.004 0.884 0.112
#&gt; ERR519488     1  0.0000    0.80555 1.000 0.000 0.000 0.000 0.000
#&gt; ERR519493     1  0.5811    0.41747 0.568 0.000 0.000 0.116 0.316
#&gt; ERR519514     1  0.0290    0.80653 0.992 0.000 0.000 0.000 0.008
#&gt; ERR519479     4  0.3561    0.57645 0.000 0.000 0.000 0.740 0.260
#&gt; ERR519509     1  0.0000    0.80555 1.000 0.000 0.000 0.000 0.000
#&gt; ERR519472     4  0.2280    0.70750 0.000 0.000 0.000 0.880 0.120
#&gt; ERR519510     5  0.4420    0.45044 0.000 0.000 0.028 0.280 0.692
#&gt; ERR519470     1  0.0290    0.80653 0.992 0.000 0.000 0.000 0.008
#&gt; ERR519495     4  0.4509    0.53571 0.048 0.000 0.000 0.716 0.236
#&gt; ERR519522     1  0.0162    0.80407 0.996 0.000 0.000 0.000 0.004
#&gt; ERR519523     4  0.2193    0.71531 0.008 0.000 0.000 0.900 0.092
#&gt; ERR519503     1  0.1121    0.78261 0.956 0.000 0.000 0.000 0.044
#&gt; ERR519471     1  0.0912    0.80184 0.972 0.000 0.000 0.012 0.016
#&gt; ERR519500     4  0.0290    0.73138 0.000 0.000 0.000 0.992 0.008
#&gt; ERR519485     1  0.5176    0.42723 0.572 0.000 0.000 0.048 0.380
#&gt; ERR519476     2  0.0510    0.99088 0.000 0.984 0.000 0.000 0.016
#&gt; ERR519502     4  0.3527    0.68455 0.000 0.000 0.024 0.804 0.172
#&gt; ERR519486     1  0.5435    0.30605 0.512 0.000 0.000 0.060 0.428
#&gt; ERR519478     1  0.0000    0.80555 1.000 0.000 0.000 0.000 0.000
#&gt; ERR519497     4  0.4840    0.51489 0.000 0.000 0.056 0.676 0.268
#&gt; ERR519467     1  0.1282    0.77973 0.952 0.000 0.000 0.044 0.004
#&gt; ERR519489     4  0.0290    0.73138 0.000 0.000 0.000 0.992 0.008
#&gt; ERR519494     3  0.2358    0.87823 0.000 0.000 0.888 0.008 0.104
#&gt; ERR519474     5  0.6671    0.33141 0.240 0.000 0.000 0.340 0.420
#&gt; ERR519505     5  0.4676    0.46059 0.000 0.000 0.208 0.072 0.720
#&gt; ERR519517     3  0.1484    0.88744 0.000 0.000 0.944 0.008 0.048
#&gt; ERR519484     5  0.4832    0.48748 0.000 0.000 0.088 0.200 0.712
#&gt; ERR519498     5  0.5490    0.45317 0.000 0.000 0.228 0.128 0.644
#&gt; ERR519490     3  0.3697    0.80953 0.000 0.000 0.820 0.080 0.100
#&gt; ERR519507     4  0.3774    0.55668 0.000 0.000 0.000 0.704 0.296
#&gt; ERR519511     5  0.4696    0.20113 0.000 0.000 0.016 0.428 0.556
#&gt; ERR519468     3  0.2561    0.88585 0.000 0.000 0.884 0.020 0.096
#&gt; ERR519482     3  0.2616    0.87160 0.000 0.000 0.880 0.020 0.100
#&gt; ERR519475     2  0.0000    0.99545 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519496     1  0.4028    0.68267 0.776 0.000 0.000 0.048 0.176
#&gt; ERR519506     5  0.5981    0.41471 0.160 0.000 0.000 0.264 0.576
#&gt; ERR519469     4  0.3409    0.69593 0.000 0.000 0.024 0.816 0.160
#&gt; ERR519480     3  0.0794    0.88844 0.000 0.000 0.972 0.000 0.028
#&gt; ERR519487     3  0.1270    0.88405 0.000 0.000 0.948 0.000 0.052
#&gt; ERR519483     5  0.6315    0.39468 0.212 0.000 0.000 0.260 0.528
#&gt; ERR519477     2  0.0000    0.99545 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519499     3  0.1270    0.88405 0.000 0.000 0.948 0.000 0.052
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-4-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-5'>
<p><a id='tab-MAD-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; ERR519515     1  0.0858     0.8053 0.968 0.000 0.000 0.000 0.004 0.028
#&gt; ERR519516     1  0.6498     0.1252 0.444 0.000 0.000 0.308 0.032 0.216
#&gt; ERR519520     4  0.4859     0.4580 0.244 0.000 0.004 0.676 0.056 0.020
#&gt; ERR519513     5  0.2282     0.6937 0.000 0.000 0.068 0.012 0.900 0.020
#&gt; ERR519481     4  0.4459     0.6773 0.000 0.000 0.132 0.756 0.044 0.068
#&gt; ERR519491     1  0.4469     0.3620 0.584 0.000 0.000 0.016 0.012 0.388
#&gt; ERR519473     4  0.5445     0.5702 0.000 0.000 0.160 0.632 0.020 0.188
#&gt; ERR519518     4  0.5399     0.4198 0.000 0.000 0.380 0.536 0.048 0.036
#&gt; ERR519512     4  0.1765     0.6957 0.000 0.000 0.000 0.924 0.052 0.024
#&gt; ERR519521     4  0.1726     0.7011 0.000 0.000 0.012 0.932 0.044 0.012
#&gt; ERR519488     1  0.0146     0.8051 0.996 0.000 0.004 0.000 0.000 0.000
#&gt; ERR519493     1  0.5309     0.2189 0.512 0.000 0.000 0.024 0.052 0.412
#&gt; ERR519514     1  0.0972     0.8048 0.964 0.000 0.000 0.000 0.008 0.028
#&gt; ERR519479     6  0.4385     0.2281 0.000 0.000 0.000 0.444 0.024 0.532
#&gt; ERR519509     1  0.0146     0.8051 0.996 0.000 0.004 0.000 0.000 0.000
#&gt; ERR519472     4  0.3799     0.5029 0.000 0.000 0.000 0.704 0.020 0.276
#&gt; ERR519510     5  0.5167     0.4873 0.000 0.000 0.008 0.092 0.600 0.300
#&gt; ERR519470     1  0.0858     0.8053 0.968 0.000 0.000 0.000 0.004 0.028
#&gt; ERR519495     6  0.4644     0.2847 0.008 0.000 0.000 0.412 0.028 0.552
#&gt; ERR519522     1  0.0748     0.7971 0.976 0.000 0.004 0.000 0.004 0.016
#&gt; ERR519523     4  0.2249     0.6889 0.004 0.000 0.000 0.900 0.064 0.032
#&gt; ERR519503     1  0.1219     0.7817 0.948 0.000 0.004 0.000 0.000 0.048
#&gt; ERR519471     1  0.1584     0.7880 0.928 0.000 0.000 0.000 0.008 0.064
#&gt; ERR519500     4  0.1444     0.7057 0.000 0.000 0.000 0.928 0.000 0.072
#&gt; ERR519485     6  0.3489     0.3135 0.288 0.000 0.000 0.000 0.004 0.708
#&gt; ERR519476     2  0.0993     0.9766 0.000 0.964 0.000 0.000 0.024 0.012
#&gt; ERR519502     4  0.3616     0.7014 0.000 0.000 0.088 0.824 0.040 0.048
#&gt; ERR519486     6  0.4599     0.3679 0.252 0.000 0.000 0.012 0.056 0.680
#&gt; ERR519478     1  0.0146     0.8051 0.996 0.000 0.004 0.000 0.000 0.000
#&gt; ERR519497     4  0.4745     0.3794 0.000 0.000 0.028 0.604 0.348 0.020
#&gt; ERR519467     1  0.1793     0.7792 0.932 0.000 0.004 0.040 0.008 0.016
#&gt; ERR519489     4  0.1501     0.7037 0.000 0.000 0.000 0.924 0.000 0.076
#&gt; ERR519494     3  0.1536     0.8277 0.000 0.000 0.940 0.004 0.016 0.040
#&gt; ERR519474     6  0.2937     0.5574 0.096 0.000 0.000 0.056 0.000 0.848
#&gt; ERR519505     5  0.2519     0.7314 0.000 0.000 0.020 0.020 0.888 0.072
#&gt; ERR519517     3  0.2994     0.8369 0.000 0.000 0.788 0.004 0.208 0.000
#&gt; ERR519484     5  0.6030     0.4981 0.000 0.000 0.100 0.064 0.568 0.268
#&gt; ERR519498     5  0.2259     0.7261 0.000 0.000 0.020 0.040 0.908 0.032
#&gt; ERR519490     3  0.1562     0.8162 0.000 0.000 0.940 0.024 0.004 0.032
#&gt; ERR519507     6  0.4546     0.3243 0.000 0.000 0.008 0.396 0.024 0.572
#&gt; ERR519511     6  0.6690    -0.0707 0.000 0.000 0.036 0.244 0.344 0.376
#&gt; ERR519468     3  0.1606     0.8422 0.000 0.000 0.932 0.008 0.056 0.004
#&gt; ERR519482     3  0.1296     0.8244 0.000 0.000 0.952 0.012 0.004 0.032
#&gt; ERR519475     2  0.0000     0.9884 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; ERR519496     1  0.4178     0.2840 0.560 0.000 0.000 0.004 0.008 0.428
#&gt; ERR519506     6  0.2059     0.5321 0.024 0.000 0.008 0.024 0.020 0.924
#&gt; ERR519469     4  0.5310     0.5755 0.000 0.000 0.140 0.648 0.020 0.192
#&gt; ERR519480     3  0.2772     0.8383 0.000 0.000 0.816 0.000 0.180 0.004
#&gt; ERR519487     3  0.2969     0.8309 0.000 0.000 0.776 0.000 0.224 0.000
#&gt; ERR519483     6  0.2094     0.5394 0.032 0.000 0.004 0.028 0.016 0.920
#&gt; ERR519477     2  0.0000     0.9884 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; ERR519499     3  0.2969     0.8309 0.000 0.000 0.776 0.000 0.224 0.000
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-5-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-get-signatures'>
<ul>
<li><a href='#tab-MAD-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-kmeans-signature_compare](figure_cola/MAD-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-kmeans-collect-classes](figure_cola/MAD-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:skmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "skmeans"]
# you can also extract it by
# res = res_list["MAD:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 18140 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-skmeans-collect-plots](figure_cola/MAD-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-skmeans-select-partition-number](figure_cola/MAD-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.959           0.953       0.980         0.5042 0.497   0.497
#> 3 3 0.790           0.874       0.929         0.3285 0.787   0.592
#> 4 4 0.705           0.787       0.874         0.1113 0.908   0.732
#> 5 5 0.680           0.616       0.792         0.0672 0.917   0.699
#> 6 6 0.719           0.590       0.738         0.0431 0.914   0.626
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-get-classes'>
<ul>
<li><a href='#tab-MAD-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-skmeans-get-classes-1'>
<p><a id='tab-MAD-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; ERR519515     2   0.000      0.981 0.000 1.000
#&gt; ERR519516     2   0.000      0.981 0.000 1.000
#&gt; ERR519520     1   0.929      0.486 0.656 0.344
#&gt; ERR519513     1   0.000      0.976 1.000 0.000
#&gt; ERR519481     1   0.000      0.976 1.000 0.000
#&gt; ERR519491     2   0.000      0.981 0.000 1.000
#&gt; ERR519473     1   0.000      0.976 1.000 0.000
#&gt; ERR519518     1   0.000      0.976 1.000 0.000
#&gt; ERR519512     1   0.184      0.951 0.972 0.028
#&gt; ERR519521     1   0.000      0.976 1.000 0.000
#&gt; ERR519488     2   0.000      0.981 0.000 1.000
#&gt; ERR519493     2   0.000      0.981 0.000 1.000
#&gt; ERR519514     2   0.000      0.981 0.000 1.000
#&gt; ERR519479     1   0.000      0.976 1.000 0.000
#&gt; ERR519509     2   0.000      0.981 0.000 1.000
#&gt; ERR519472     1   0.000      0.976 1.000 0.000
#&gt; ERR519510     1   0.000      0.976 1.000 0.000
#&gt; ERR519470     2   0.000      0.981 0.000 1.000
#&gt; ERR519495     2   0.595      0.823 0.144 0.856
#&gt; ERR519522     2   0.000      0.981 0.000 1.000
#&gt; ERR519523     1   0.844      0.629 0.728 0.272
#&gt; ERR519503     2   0.000      0.981 0.000 1.000
#&gt; ERR519471     2   0.000      0.981 0.000 1.000
#&gt; ERR519500     1   0.000      0.976 1.000 0.000
#&gt; ERR519485     2   0.000      0.981 0.000 1.000
#&gt; ERR519476     2   0.000      0.981 0.000 1.000
#&gt; ERR519502     1   0.000      0.976 1.000 0.000
#&gt; ERR519486     2   0.000      0.981 0.000 1.000
#&gt; ERR519478     2   0.000      0.981 0.000 1.000
#&gt; ERR519497     1   0.000      0.976 1.000 0.000
#&gt; ERR519467     2   0.000      0.981 0.000 1.000
#&gt; ERR519489     1   0.000      0.976 1.000 0.000
#&gt; ERR519494     1   0.000      0.976 1.000 0.000
#&gt; ERR519474     2   0.000      0.981 0.000 1.000
#&gt; ERR519505     1   0.000      0.976 1.000 0.000
#&gt; ERR519517     1   0.000      0.976 1.000 0.000
#&gt; ERR519484     1   0.000      0.976 1.000 0.000
#&gt; ERR519498     1   0.000      0.976 1.000 0.000
#&gt; ERR519490     1   0.000      0.976 1.000 0.000
#&gt; ERR519507     1   0.000      0.976 1.000 0.000
#&gt; ERR519511     1   0.000      0.976 1.000 0.000
#&gt; ERR519468     1   0.000      0.976 1.000 0.000
#&gt; ERR519482     1   0.000      0.976 1.000 0.000
#&gt; ERR519475     2   0.000      0.981 0.000 1.000
#&gt; ERR519496     2   0.000      0.981 0.000 1.000
#&gt; ERR519506     2   0.802      0.672 0.244 0.756
#&gt; ERR519469     1   0.000      0.976 1.000 0.000
#&gt; ERR519480     1   0.000      0.976 1.000 0.000
#&gt; ERR519487     1   0.000      0.976 1.000 0.000
#&gt; ERR519483     2   0.000      0.981 0.000 1.000
#&gt; ERR519477     2   0.000      0.981 0.000 1.000
#&gt; ERR519499     1   0.000      0.976 1.000 0.000
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-1-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-2'>
<p><a id='tab-MAD-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; ERR519515     2  0.0000      0.957 0.000 1.000 0.000
#&gt; ERR519516     2  0.4654      0.755 0.208 0.792 0.000
#&gt; ERR519520     1  0.4353      0.771 0.836 0.156 0.008
#&gt; ERR519513     3  0.0000      0.987 0.000 0.000 1.000
#&gt; ERR519481     1  0.3816      0.801 0.852 0.000 0.148
#&gt; ERR519491     2  0.0000      0.957 0.000 1.000 0.000
#&gt; ERR519473     1  0.2356      0.836 0.928 0.000 0.072
#&gt; ERR519518     3  0.1289      0.970 0.032 0.000 0.968
#&gt; ERR519512     1  0.1453      0.842 0.968 0.008 0.024
#&gt; ERR519521     1  0.1031      0.844 0.976 0.000 0.024
#&gt; ERR519488     2  0.0000      0.957 0.000 1.000 0.000
#&gt; ERR519493     2  0.0424      0.956 0.008 0.992 0.000
#&gt; ERR519514     2  0.0000      0.957 0.000 1.000 0.000
#&gt; ERR519479     1  0.0424      0.840 0.992 0.000 0.008
#&gt; ERR519509     2  0.0000      0.957 0.000 1.000 0.000
#&gt; ERR519472     1  0.1031      0.844 0.976 0.000 0.024
#&gt; ERR519510     1  0.5835      0.585 0.660 0.000 0.340
#&gt; ERR519470     2  0.0000      0.957 0.000 1.000 0.000
#&gt; ERR519495     1  0.4002      0.775 0.840 0.160 0.000
#&gt; ERR519522     2  0.0000      0.957 0.000 1.000 0.000
#&gt; ERR519523     1  0.1411      0.832 0.964 0.036 0.000
#&gt; ERR519503     2  0.0237      0.957 0.004 0.996 0.000
#&gt; ERR519471     2  0.0000      0.957 0.000 1.000 0.000
#&gt; ERR519500     1  0.1031      0.844 0.976 0.000 0.024
#&gt; ERR519485     2  0.0747      0.953 0.016 0.984 0.000
#&gt; ERR519476     2  0.1620      0.944 0.024 0.964 0.012
#&gt; ERR519502     1  0.4062      0.790 0.836 0.000 0.164
#&gt; ERR519486     2  0.0592      0.954 0.012 0.988 0.000
#&gt; ERR519478     2  0.0000      0.957 0.000 1.000 0.000
#&gt; ERR519497     3  0.0592      0.989 0.012 0.000 0.988
#&gt; ERR519467     2  0.1753      0.927 0.048 0.952 0.000
#&gt; ERR519489     1  0.1031      0.844 0.976 0.000 0.024
#&gt; ERR519494     3  0.0237      0.990 0.004 0.000 0.996
#&gt; ERR519474     1  0.5291      0.570 0.732 0.268 0.000
#&gt; ERR519505     3  0.1031      0.964 0.024 0.000 0.976
#&gt; ERR519517     3  0.0592      0.989 0.012 0.000 0.988
#&gt; ERR519484     1  0.6295      0.279 0.528 0.000 0.472
#&gt; ERR519498     3  0.0000      0.987 0.000 0.000 1.000
#&gt; ERR519490     3  0.0592      0.989 0.012 0.000 0.988
#&gt; ERR519507     1  0.2066      0.837 0.940 0.000 0.060
#&gt; ERR519511     1  0.5678      0.621 0.684 0.000 0.316
#&gt; ERR519468     3  0.0592      0.989 0.012 0.000 0.988
#&gt; ERR519482     3  0.0592      0.989 0.012 0.000 0.988
#&gt; ERR519475     2  0.1620      0.944 0.024 0.964 0.012
#&gt; ERR519496     2  0.0000      0.957 0.000 1.000 0.000
#&gt; ERR519506     2  0.8321      0.560 0.148 0.624 0.228
#&gt; ERR519469     1  0.5810      0.530 0.664 0.000 0.336
#&gt; ERR519480     3  0.0237      0.990 0.004 0.000 0.996
#&gt; ERR519487     3  0.0237      0.990 0.004 0.000 0.996
#&gt; ERR519483     2  0.3340      0.872 0.120 0.880 0.000
#&gt; ERR519477     2  0.1620      0.944 0.024 0.964 0.012
#&gt; ERR519499     3  0.0237      0.990 0.004 0.000 0.996
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-2-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-3'>
<p><a id='tab-MAD-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; ERR519515     1  0.0188      0.882 0.996 0.004 0.000 0.000
#&gt; ERR519516     1  0.5035      0.669 0.744 0.052 0.000 0.204
#&gt; ERR519520     1  0.4522      0.541 0.680 0.000 0.000 0.320
#&gt; ERR519513     3  0.0657      0.944 0.000 0.012 0.984 0.004
#&gt; ERR519481     4  0.3182      0.797 0.000 0.028 0.096 0.876
#&gt; ERR519491     1  0.0188      0.882 0.996 0.004 0.000 0.000
#&gt; ERR519473     4  0.3215      0.801 0.000 0.092 0.032 0.876
#&gt; ERR519518     3  0.2060      0.910 0.000 0.016 0.932 0.052
#&gt; ERR519512     4  0.1151      0.795 0.024 0.000 0.008 0.968
#&gt; ERR519521     4  0.0592      0.801 0.000 0.000 0.016 0.984
#&gt; ERR519488     1  0.0469      0.879 0.988 0.012 0.000 0.000
#&gt; ERR519493     1  0.2973      0.775 0.856 0.144 0.000 0.000
#&gt; ERR519514     1  0.0188      0.882 0.996 0.004 0.000 0.000
#&gt; ERR519479     4  0.2589      0.798 0.000 0.116 0.000 0.884
#&gt; ERR519509     1  0.0469      0.879 0.988 0.012 0.000 0.000
#&gt; ERR519472     4  0.2334      0.800 0.000 0.088 0.004 0.908
#&gt; ERR519510     4  0.7325      0.505 0.000 0.208 0.264 0.528
#&gt; ERR519470     1  0.0188      0.882 0.996 0.004 0.000 0.000
#&gt; ERR519495     4  0.5080      0.714 0.144 0.092 0.000 0.764
#&gt; ERR519522     1  0.0188      0.881 0.996 0.004 0.000 0.000
#&gt; ERR519523     4  0.1940      0.769 0.076 0.000 0.000 0.924
#&gt; ERR519503     1  0.4072      0.565 0.748 0.252 0.000 0.000
#&gt; ERR519471     1  0.0188      0.882 0.996 0.004 0.000 0.000
#&gt; ERR519500     4  0.0336      0.801 0.000 0.000 0.008 0.992
#&gt; ERR519485     2  0.4981      0.250 0.464 0.536 0.000 0.000
#&gt; ERR519476     2  0.2814      0.844 0.132 0.868 0.000 0.000
#&gt; ERR519502     4  0.3160      0.793 0.000 0.020 0.108 0.872
#&gt; ERR519486     1  0.4164      0.556 0.736 0.264 0.000 0.000
#&gt; ERR519478     1  0.0188      0.881 0.996 0.004 0.000 0.000
#&gt; ERR519497     3  0.0188      0.949 0.000 0.000 0.996 0.004
#&gt; ERR519467     1  0.2216      0.818 0.908 0.000 0.000 0.092
#&gt; ERR519489     4  0.0336      0.801 0.000 0.000 0.008 0.992
#&gt; ERR519494     3  0.0707      0.947 0.000 0.020 0.980 0.000
#&gt; ERR519474     4  0.6031      0.605 0.144 0.168 0.000 0.688
#&gt; ERR519505     3  0.4855      0.479 0.000 0.352 0.644 0.004
#&gt; ERR519517     3  0.0000      0.949 0.000 0.000 1.000 0.000
#&gt; ERR519484     4  0.7597      0.428 0.000 0.224 0.308 0.468
#&gt; ERR519498     3  0.0524      0.946 0.000 0.008 0.988 0.004
#&gt; ERR519490     3  0.1820      0.921 0.000 0.020 0.944 0.036
#&gt; ERR519507     4  0.3894      0.790 0.004 0.140 0.024 0.832
#&gt; ERR519511     4  0.7088      0.560 0.000 0.228 0.204 0.568
#&gt; ERR519468     3  0.0895      0.944 0.000 0.020 0.976 0.004
#&gt; ERR519482     3  0.1042      0.942 0.000 0.020 0.972 0.008
#&gt; ERR519475     2  0.2814      0.844 0.132 0.868 0.000 0.000
#&gt; ERR519496     1  0.0921      0.870 0.972 0.028 0.000 0.000
#&gt; ERR519506     2  0.0927      0.761 0.008 0.976 0.000 0.016
#&gt; ERR519469     4  0.6411      0.513 0.000 0.092 0.308 0.600
#&gt; ERR519480     3  0.0188      0.949 0.000 0.004 0.996 0.000
#&gt; ERR519487     3  0.0000      0.949 0.000 0.000 1.000 0.000
#&gt; ERR519483     2  0.2796      0.798 0.092 0.892 0.000 0.016
#&gt; ERR519477     2  0.2814      0.844 0.132 0.868 0.000 0.000
#&gt; ERR519499     3  0.0000      0.949 0.000 0.000 1.000 0.000
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-3-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-4'>
<p><a id='tab-MAD-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; ERR519515     1  0.0609     0.8354 0.980 0.000 0.000 0.000 0.020
#&gt; ERR519516     1  0.7100     0.4430 0.540 0.064 0.000 0.236 0.160
#&gt; ERR519520     4  0.4588     0.1877 0.380 0.000 0.000 0.604 0.016
#&gt; ERR519513     3  0.4029     0.5327 0.000 0.000 0.680 0.004 0.316
#&gt; ERR519481     4  0.4700     0.5747 0.000 0.000 0.088 0.728 0.184
#&gt; ERR519491     1  0.2674     0.7625 0.856 0.004 0.000 0.000 0.140
#&gt; ERR519473     4  0.4194     0.5884 0.000 0.012 0.004 0.708 0.276
#&gt; ERR519518     3  0.4555     0.5880 0.000 0.000 0.720 0.224 0.056
#&gt; ERR519512     4  0.1179     0.6855 0.016 0.000 0.004 0.964 0.016
#&gt; ERR519521     4  0.0404     0.6936 0.000 0.000 0.000 0.988 0.012
#&gt; ERR519488     1  0.0290     0.8344 0.992 0.008 0.000 0.000 0.000
#&gt; ERR519493     1  0.6259     0.4180 0.540 0.212 0.000 0.000 0.248
#&gt; ERR519514     1  0.0609     0.8354 0.980 0.000 0.000 0.000 0.020
#&gt; ERR519479     5  0.4648    -0.1862 0.000 0.012 0.000 0.464 0.524
#&gt; ERR519509     1  0.0290     0.8344 0.992 0.008 0.000 0.000 0.000
#&gt; ERR519472     4  0.3988     0.6042 0.000 0.016 0.000 0.732 0.252
#&gt; ERR519510     5  0.3759     0.4944 0.000 0.012 0.148 0.028 0.812
#&gt; ERR519470     1  0.0609     0.8354 0.980 0.000 0.000 0.000 0.020
#&gt; ERR519495     4  0.6436     0.2901 0.132 0.016 0.000 0.528 0.324
#&gt; ERR519522     1  0.0290     0.8344 0.992 0.008 0.000 0.000 0.000
#&gt; ERR519523     4  0.1300     0.6827 0.028 0.000 0.000 0.956 0.016
#&gt; ERR519503     1  0.3730     0.4938 0.712 0.288 0.000 0.000 0.000
#&gt; ERR519471     1  0.0898     0.8334 0.972 0.008 0.000 0.000 0.020
#&gt; ERR519500     4  0.0609     0.6971 0.000 0.000 0.000 0.980 0.020
#&gt; ERR519485     2  0.5395     0.3709 0.356 0.576 0.000 0.000 0.068
#&gt; ERR519476     2  0.0898     0.8117 0.020 0.972 0.000 0.000 0.008
#&gt; ERR519502     4  0.4609     0.5795 0.000 0.000 0.104 0.744 0.152
#&gt; ERR519486     1  0.5925     0.2837 0.472 0.104 0.000 0.000 0.424
#&gt; ERR519478     1  0.0290     0.8344 0.992 0.008 0.000 0.000 0.000
#&gt; ERR519497     3  0.3033     0.7888 0.000 0.000 0.864 0.052 0.084
#&gt; ERR519467     1  0.2389     0.7624 0.880 0.000 0.000 0.116 0.004
#&gt; ERR519489     4  0.0566     0.6976 0.000 0.000 0.012 0.984 0.004
#&gt; ERR519494     3  0.1478     0.8440 0.000 0.000 0.936 0.000 0.064
#&gt; ERR519474     5  0.7237     0.0504 0.112 0.076 0.000 0.348 0.464
#&gt; ERR519505     5  0.6708    -0.1442 0.000 0.164 0.396 0.012 0.428
#&gt; ERR519517     3  0.0000     0.8509 0.000 0.000 1.000 0.000 0.000
#&gt; ERR519484     5  0.3314     0.5106 0.000 0.012 0.124 0.020 0.844
#&gt; ERR519498     3  0.4430     0.4559 0.000 0.000 0.628 0.012 0.360
#&gt; ERR519490     3  0.1914     0.8367 0.000 0.000 0.924 0.016 0.060
#&gt; ERR519507     5  0.4723    -0.1565 0.000 0.016 0.000 0.448 0.536
#&gt; ERR519511     5  0.3478     0.5261 0.000 0.016 0.096 0.040 0.848
#&gt; ERR519468     3  0.1357     0.8463 0.000 0.000 0.948 0.004 0.048
#&gt; ERR519482     3  0.1697     0.8411 0.000 0.000 0.932 0.008 0.060
#&gt; ERR519475     2  0.0898     0.8117 0.020 0.972 0.000 0.000 0.008
#&gt; ERR519496     1  0.1106     0.8315 0.964 0.012 0.000 0.000 0.024
#&gt; ERR519506     2  0.3087     0.7427 0.008 0.836 0.000 0.004 0.152
#&gt; ERR519469     4  0.5672     0.5474 0.000 0.012 0.120 0.656 0.212
#&gt; ERR519480     3  0.0162     0.8511 0.000 0.000 0.996 0.000 0.004
#&gt; ERR519487     3  0.0000     0.8509 0.000 0.000 1.000 0.000 0.000
#&gt; ERR519483     2  0.3911     0.7428 0.060 0.796 0.000 0.000 0.144
#&gt; ERR519477     2  0.0898     0.8117 0.020 0.972 0.000 0.000 0.008
#&gt; ERR519499     3  0.0000     0.8509 0.000 0.000 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-4-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-5'>
<p><a id='tab-MAD-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; ERR519515     1  0.0146     0.8342 0.996 0.000 0.000 0.004 0.000 0.000
#&gt; ERR519516     4  0.7499    -0.1402 0.356 0.180 0.000 0.360 0.032 0.072
#&gt; ERR519520     4  0.4079     0.5145 0.140 0.000 0.000 0.760 0.096 0.004
#&gt; ERR519513     6  0.4242     0.3730 0.000 0.000 0.448 0.016 0.000 0.536
#&gt; ERR519481     5  0.5954     0.2605 0.000 0.000 0.076 0.216 0.604 0.104
#&gt; ERR519491     1  0.3357     0.7505 0.848 0.008 0.000 0.064 0.020 0.060
#&gt; ERR519473     5  0.2721     0.5173 0.000 0.000 0.040 0.088 0.868 0.004
#&gt; ERR519518     3  0.5885     0.4560 0.000 0.000 0.596 0.228 0.128 0.048
#&gt; ERR519512     4  0.3023     0.6313 0.000 0.000 0.000 0.768 0.232 0.000
#&gt; ERR519521     4  0.3489     0.6236 0.000 0.000 0.000 0.708 0.288 0.004
#&gt; ERR519488     1  0.1515     0.8290 0.944 0.020 0.000 0.028 0.000 0.008
#&gt; ERR519493     1  0.7152     0.2621 0.472 0.260 0.000 0.076 0.020 0.172
#&gt; ERR519514     1  0.0146     0.8342 0.996 0.000 0.000 0.004 0.000 0.000
#&gt; ERR519479     5  0.2902     0.5480 0.000 0.000 0.000 0.004 0.800 0.196
#&gt; ERR519509     1  0.1515     0.8290 0.944 0.020 0.000 0.028 0.000 0.008
#&gt; ERR519472     5  0.2278     0.4919 0.000 0.000 0.004 0.128 0.868 0.000
#&gt; ERR519510     6  0.2658     0.6473 0.000 0.000 0.036 0.000 0.100 0.864
#&gt; ERR519470     1  0.0146     0.8342 0.996 0.000 0.000 0.004 0.000 0.000
#&gt; ERR519495     5  0.3891     0.5115 0.112 0.000 0.000 0.036 0.800 0.052
#&gt; ERR519522     1  0.1116     0.8318 0.960 0.004 0.000 0.028 0.000 0.008
#&gt; ERR519523     4  0.3560     0.6338 0.008 0.000 0.000 0.732 0.256 0.004
#&gt; ERR519503     1  0.4108     0.5720 0.704 0.260 0.000 0.028 0.000 0.008
#&gt; ERR519471     1  0.0551     0.8311 0.984 0.008 0.000 0.004 0.000 0.004
#&gt; ERR519500     4  0.3955     0.4494 0.000 0.000 0.000 0.560 0.436 0.004
#&gt; ERR519485     2  0.7878     0.3244 0.292 0.368 0.000 0.200 0.044 0.096
#&gt; ERR519476     2  0.0405     0.7054 0.008 0.988 0.000 0.000 0.000 0.004
#&gt; ERR519502     5  0.6383     0.0794 0.000 0.000 0.064 0.280 0.520 0.136
#&gt; ERR519486     1  0.7934    -0.0619 0.356 0.080 0.000 0.216 0.056 0.292
#&gt; ERR519478     1  0.1116     0.8318 0.960 0.004 0.000 0.028 0.000 0.008
#&gt; ERR519497     3  0.6331     0.2612 0.000 0.000 0.508 0.256 0.036 0.200
#&gt; ERR519467     1  0.2513     0.7669 0.852 0.000 0.000 0.140 0.000 0.008
#&gt; ERR519489     4  0.3899     0.5190 0.000 0.000 0.000 0.592 0.404 0.004
#&gt; ERR519494     3  0.1863     0.8089 0.000 0.000 0.920 0.000 0.036 0.044
#&gt; ERR519474     5  0.7600     0.0996 0.080 0.032 0.000 0.288 0.396 0.204
#&gt; ERR519505     6  0.5399     0.6256 0.000 0.088 0.212 0.048 0.000 0.652
#&gt; ERR519517     3  0.0935     0.8164 0.000 0.000 0.964 0.000 0.004 0.032
#&gt; ERR519484     6  0.3248     0.6306 0.000 0.000 0.052 0.004 0.116 0.828
#&gt; ERR519498     6  0.4594     0.5413 0.000 0.000 0.340 0.052 0.000 0.608
#&gt; ERR519490     3  0.2001     0.8044 0.000 0.000 0.912 0.000 0.048 0.040
#&gt; ERR519507     5  0.3245     0.5509 0.000 0.000 0.004 0.016 0.796 0.184
#&gt; ERR519511     6  0.3522     0.5737 0.000 0.000 0.044 0.000 0.172 0.784
#&gt; ERR519468     3  0.0713     0.8192 0.000 0.000 0.972 0.000 0.028 0.000
#&gt; ERR519482     3  0.1934     0.8068 0.000 0.000 0.916 0.000 0.044 0.040
#&gt; ERR519475     2  0.0405     0.7054 0.008 0.988 0.000 0.000 0.000 0.004
#&gt; ERR519496     1  0.2666     0.7827 0.892 0.008 0.000 0.032 0.044 0.024
#&gt; ERR519506     2  0.6346     0.5999 0.008 0.592 0.000 0.136 0.180 0.084
#&gt; ERR519469     5  0.4389     0.4296 0.000 0.000 0.188 0.100 0.712 0.000
#&gt; ERR519480     3  0.0713     0.8160 0.000 0.000 0.972 0.000 0.000 0.028
#&gt; ERR519487     3  0.0790     0.8144 0.000 0.000 0.968 0.000 0.000 0.032
#&gt; ERR519483     2  0.6762     0.5995 0.032 0.576 0.000 0.144 0.164 0.084
#&gt; ERR519477     2  0.0405     0.7054 0.008 0.988 0.000 0.000 0.000 0.004
#&gt; ERR519499     3  0.0790     0.8144 0.000 0.000 0.968 0.000 0.000 0.032
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-5-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-get-signatures'>
<ul>
<li><a href='#tab-MAD-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-skmeans-signature_compare](figure_cola/MAD-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-skmeans-collect-classes](figure_cola/MAD-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:pam






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "pam"]
# you can also extract it by
# res = res_list["MAD:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 18140 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 5.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-pam-collect-plots](figure_cola/MAD-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-pam-select-partition-number](figure_cola/MAD-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.705           0.943       0.940         0.1566 0.889   0.889
#> 3 3 0.627           0.844       0.921         1.9545 0.706   0.669
#> 4 4 0.724           0.882       0.929         0.4021 0.753   0.590
#> 5 5 0.808           0.883       0.927         0.1949 0.760   0.421
#> 6 6 0.855           0.853       0.923         0.0425 0.962   0.832
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 5
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-get-classes'>
<ul>
<li><a href='#tab-MAD-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-pam-get-classes-1'>
<p><a id='tab-MAD-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; ERR519515     1  0.1843      0.942 0.972 0.028
#&gt; ERR519516     1  0.0000      0.947 1.000 0.000
#&gt; ERR519520     1  0.1633      0.943 0.976 0.024
#&gt; ERR519513     1  0.4562      0.930 0.904 0.096
#&gt; ERR519481     1  0.4562      0.930 0.904 0.096
#&gt; ERR519491     1  0.1843      0.942 0.972 0.028
#&gt; ERR519473     1  0.4562      0.930 0.904 0.096
#&gt; ERR519518     1  0.4562      0.930 0.904 0.096
#&gt; ERR519512     1  0.2948      0.943 0.948 0.052
#&gt; ERR519521     1  0.4562      0.930 0.904 0.096
#&gt; ERR519488     1  0.1843      0.942 0.972 0.028
#&gt; ERR519493     1  0.0376      0.946 0.996 0.004
#&gt; ERR519514     1  0.1843      0.942 0.972 0.028
#&gt; ERR519479     1  0.2423      0.945 0.960 0.040
#&gt; ERR519509     1  0.1843      0.942 0.972 0.028
#&gt; ERR519472     1  0.0000      0.947 1.000 0.000
#&gt; ERR519510     1  0.2778      0.944 0.952 0.048
#&gt; ERR519470     1  0.1843      0.942 0.972 0.028
#&gt; ERR519495     1  0.1843      0.942 0.972 0.028
#&gt; ERR519522     1  0.1843      0.942 0.972 0.028
#&gt; ERR519523     1  0.1843      0.942 0.972 0.028
#&gt; ERR519503     1  0.1843      0.942 0.972 0.028
#&gt; ERR519471     1  0.1843      0.942 0.972 0.028
#&gt; ERR519500     1  0.0000      0.947 1.000 0.000
#&gt; ERR519485     1  0.1843      0.942 0.972 0.028
#&gt; ERR519476     2  0.4431      1.000 0.092 0.908
#&gt; ERR519502     1  0.4562      0.930 0.904 0.096
#&gt; ERR519486     1  0.1843      0.942 0.972 0.028
#&gt; ERR519478     1  0.1843      0.942 0.972 0.028
#&gt; ERR519497     1  0.4562      0.930 0.904 0.096
#&gt; ERR519467     1  0.1843      0.942 0.972 0.028
#&gt; ERR519489     1  0.1184      0.947 0.984 0.016
#&gt; ERR519494     1  0.4562      0.930 0.904 0.096
#&gt; ERR519474     1  0.0376      0.946 0.996 0.004
#&gt; ERR519505     1  0.2778      0.944 0.952 0.048
#&gt; ERR519517     1  0.4562      0.930 0.904 0.096
#&gt; ERR519484     1  0.3431      0.940 0.936 0.064
#&gt; ERR519498     1  0.4562      0.930 0.904 0.096
#&gt; ERR519490     1  0.4562      0.930 0.904 0.096
#&gt; ERR519507     1  0.2236      0.946 0.964 0.036
#&gt; ERR519511     1  0.3114      0.942 0.944 0.056
#&gt; ERR519468     1  0.4431      0.931 0.908 0.092
#&gt; ERR519482     1  0.4562      0.930 0.904 0.096
#&gt; ERR519475     2  0.4431      1.000 0.092 0.908
#&gt; ERR519496     1  0.1843      0.942 0.972 0.028
#&gt; ERR519506     1  0.0672      0.947 0.992 0.008
#&gt; ERR519469     1  0.0376      0.946 0.996 0.004
#&gt; ERR519480     1  0.4562      0.930 0.904 0.096
#&gt; ERR519487     1  0.4562      0.930 0.904 0.096
#&gt; ERR519483     1  0.1843      0.942 0.972 0.028
#&gt; ERR519477     2  0.4431      1.000 0.092 0.908
#&gt; ERR519499     1  0.4562      0.930 0.904 0.096
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-1-a').click(function(){
  $('#tab-MAD-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-2'>
<p><a id='tab-MAD-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3
#&gt; ERR519515     1  0.0000      0.882 1.000  0 0.000
#&gt; ERR519516     1  0.0424      0.881 0.992  0 0.008
#&gt; ERR519520     1  0.0237      0.881 0.996  0 0.004
#&gt; ERR519513     3  0.0000      1.000 0.000  0 1.000
#&gt; ERR519481     1  0.6235      0.440 0.564  0 0.436
#&gt; ERR519491     1  0.0000      0.882 1.000  0 0.000
#&gt; ERR519473     1  0.6235      0.440 0.564  0 0.436
#&gt; ERR519518     3  0.0000      1.000 0.000  0 1.000
#&gt; ERR519512     1  0.5650      0.627 0.688  0 0.312
#&gt; ERR519521     1  0.6235      0.440 0.564  0 0.436
#&gt; ERR519488     1  0.0000      0.882 1.000  0 0.000
#&gt; ERR519493     1  0.1289      0.876 0.968  0 0.032
#&gt; ERR519514     1  0.0000      0.882 1.000  0 0.000
#&gt; ERR519479     1  0.3116      0.842 0.892  0 0.108
#&gt; ERR519509     1  0.0000      0.882 1.000  0 0.000
#&gt; ERR519472     1  0.0747      0.880 0.984  0 0.016
#&gt; ERR519510     1  0.3267      0.838 0.884  0 0.116
#&gt; ERR519470     1  0.0000      0.882 1.000  0 0.000
#&gt; ERR519495     1  0.0000      0.882 1.000  0 0.000
#&gt; ERR519522     1  0.0000      0.882 1.000  0 0.000
#&gt; ERR519523     1  0.0000      0.882 1.000  0 0.000
#&gt; ERR519503     1  0.0000      0.882 1.000  0 0.000
#&gt; ERR519471     1  0.0000      0.882 1.000  0 0.000
#&gt; ERR519500     1  0.1031      0.879 0.976  0 0.024
#&gt; ERR519485     1  0.0000      0.882 1.000  0 0.000
#&gt; ERR519476     2  0.0000      1.000 0.000  1 0.000
#&gt; ERR519502     1  0.6235      0.440 0.564  0 0.436
#&gt; ERR519486     1  0.0000      0.882 1.000  0 0.000
#&gt; ERR519478     1  0.0000      0.882 1.000  0 0.000
#&gt; ERR519497     1  0.6235      0.440 0.564  0 0.436
#&gt; ERR519467     1  0.0000      0.882 1.000  0 0.000
#&gt; ERR519489     1  0.2261      0.862 0.932  0 0.068
#&gt; ERR519494     3  0.0000      1.000 0.000  0 1.000
#&gt; ERR519474     1  0.0424      0.881 0.992  0 0.008
#&gt; ERR519505     1  0.3482      0.830 0.872  0 0.128
#&gt; ERR519517     3  0.0000      1.000 0.000  0 1.000
#&gt; ERR519484     1  0.6111      0.515 0.604  0 0.396
#&gt; ERR519498     1  0.6095      0.522 0.608  0 0.392
#&gt; ERR519490     3  0.0000      1.000 0.000  0 1.000
#&gt; ERR519507     1  0.2959      0.847 0.900  0 0.100
#&gt; ERR519511     1  0.4178      0.795 0.828  0 0.172
#&gt; ERR519468     3  0.0000      1.000 0.000  0 1.000
#&gt; ERR519482     3  0.0000      1.000 0.000  0 1.000
#&gt; ERR519475     2  0.0000      1.000 0.000  1 0.000
#&gt; ERR519496     1  0.0000      0.882 1.000  0 0.000
#&gt; ERR519506     1  0.1411      0.874 0.964  0 0.036
#&gt; ERR519469     1  0.1163      0.878 0.972  0 0.028
#&gt; ERR519480     3  0.0000      1.000 0.000  0 1.000
#&gt; ERR519487     3  0.0000      1.000 0.000  0 1.000
#&gt; ERR519483     1  0.0000      0.882 1.000  0 0.000
#&gt; ERR519477     2  0.0000      1.000 0.000  1 0.000
#&gt; ERR519499     3  0.0000      1.000 0.000  0 1.000
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-2-a').click(function(){
  $('#tab-MAD-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-3'>
<p><a id='tab-MAD-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3    p4
#&gt; ERR519515     1  0.0000      0.908 1.000  0 0.000 0.000
#&gt; ERR519516     1  0.3024      0.870 0.852  0 0.000 0.148
#&gt; ERR519520     1  0.0707      0.905 0.980  0 0.000 0.020
#&gt; ERR519513     4  0.4008      0.722 0.000  0 0.244 0.756
#&gt; ERR519481     4  0.0469      0.907 0.000  0 0.012 0.988
#&gt; ERR519491     1  0.0336      0.908 0.992  0 0.000 0.008
#&gt; ERR519473     1  0.4228      0.805 0.760  0 0.008 0.232
#&gt; ERR519518     3  0.3688      0.728 0.000  0 0.792 0.208
#&gt; ERR519512     1  0.3636      0.859 0.820  0 0.008 0.172
#&gt; ERR519521     4  0.2011      0.875 0.000  0 0.080 0.920
#&gt; ERR519488     1  0.0000      0.908 1.000  0 0.000 0.000
#&gt; ERR519493     1  0.4277      0.746 0.720  0 0.000 0.280
#&gt; ERR519514     1  0.0000      0.908 1.000  0 0.000 0.000
#&gt; ERR519479     4  0.0707      0.903 0.020  0 0.000 0.980
#&gt; ERR519509     1  0.0000      0.908 1.000  0 0.000 0.000
#&gt; ERR519472     1  0.3266      0.861 0.832  0 0.000 0.168
#&gt; ERR519510     4  0.0707      0.903 0.020  0 0.000 0.980
#&gt; ERR519470     1  0.0000      0.908 1.000  0 0.000 0.000
#&gt; ERR519495     1  0.0469      0.908 0.988  0 0.000 0.012
#&gt; ERR519522     1  0.0000      0.908 1.000  0 0.000 0.000
#&gt; ERR519523     1  0.3266      0.864 0.832  0 0.000 0.168
#&gt; ERR519503     1  0.0000      0.908 1.000  0 0.000 0.000
#&gt; ERR519471     1  0.0469      0.908 0.988  0 0.000 0.012
#&gt; ERR519500     1  0.3494      0.859 0.824  0 0.004 0.172
#&gt; ERR519485     1  0.0469      0.908 0.988  0 0.000 0.012
#&gt; ERR519476     2  0.0000      1.000 0.000  1 0.000 0.000
#&gt; ERR519502     4  0.0592      0.907 0.000  0 0.016 0.984
#&gt; ERR519486     1  0.1867      0.875 0.928  0 0.000 0.072
#&gt; ERR519478     1  0.0000      0.908 1.000  0 0.000 0.000
#&gt; ERR519497     4  0.0927      0.909 0.008  0 0.016 0.976
#&gt; ERR519467     1  0.0000      0.908 1.000  0 0.000 0.000
#&gt; ERR519489     1  0.4610      0.798 0.744  0 0.020 0.236
#&gt; ERR519494     3  0.2011      0.867 0.000  0 0.920 0.080
#&gt; ERR519474     1  0.3528      0.849 0.808  0 0.000 0.192
#&gt; ERR519505     4  0.3428      0.807 0.012  0 0.144 0.844
#&gt; ERR519517     3  0.0000      0.919 0.000  0 1.000 0.000
#&gt; ERR519484     4  0.0937      0.910 0.012  0 0.012 0.976
#&gt; ERR519498     4  0.4175      0.756 0.012  0 0.212 0.776
#&gt; ERR519490     3  0.3024      0.784 0.000  0 0.852 0.148
#&gt; ERR519507     4  0.0817      0.900 0.024  0 0.000 0.976
#&gt; ERR519511     4  0.0804      0.909 0.012  0 0.008 0.980
#&gt; ERR519468     3  0.0000      0.919 0.000  0 1.000 0.000
#&gt; ERR519482     3  0.0336      0.916 0.000  0 0.992 0.008
#&gt; ERR519475     2  0.0000      1.000 0.000  1 0.000 0.000
#&gt; ERR519496     1  0.0336      0.908 0.992  0 0.000 0.008
#&gt; ERR519506     1  0.3801      0.824 0.780  0 0.000 0.220
#&gt; ERR519469     1  0.3539      0.858 0.820  0 0.004 0.176
#&gt; ERR519480     3  0.0000      0.919 0.000  0 1.000 0.000
#&gt; ERR519487     3  0.0000      0.919 0.000  0 1.000 0.000
#&gt; ERR519483     1  0.0592      0.908 0.984  0 0.000 0.016
#&gt; ERR519477     2  0.0000      1.000 0.000  1 0.000 0.000
#&gt; ERR519499     3  0.0000      0.919 0.000  0 1.000 0.000
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-3-a').click(function(){
  $('#tab-MAD-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-4'>
<p><a id='tab-MAD-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3    p4    p5
#&gt; ERR519515     1  0.0000      0.952 1.000  0 0.000 0.000 0.000
#&gt; ERR519516     1  0.3795      0.786 0.780  0 0.000 0.192 0.028
#&gt; ERR519520     4  0.1270      0.847 0.052  0 0.000 0.948 0.000
#&gt; ERR519513     5  0.3177      0.788 0.000  0 0.208 0.000 0.792
#&gt; ERR519481     5  0.0290      0.866 0.000  0 0.000 0.008 0.992
#&gt; ERR519491     1  0.1484      0.940 0.944  0 0.000 0.048 0.008
#&gt; ERR519473     4  0.5848      0.613 0.000  0 0.192 0.608 0.200
#&gt; ERR519518     4  0.2488      0.825 0.000  0 0.004 0.872 0.124
#&gt; ERR519512     4  0.0290      0.861 0.000  0 0.000 0.992 0.008
#&gt; ERR519521     4  0.2685      0.819 0.000  0 0.028 0.880 0.092
#&gt; ERR519488     1  0.0000      0.952 1.000  0 0.000 0.000 0.000
#&gt; ERR519493     5  0.4316      0.770 0.120  0 0.000 0.108 0.772
#&gt; ERR519514     1  0.0000      0.952 1.000  0 0.000 0.000 0.000
#&gt; ERR519479     5  0.1908      0.876 0.000  0 0.000 0.092 0.908
#&gt; ERR519509     1  0.0000      0.952 1.000  0 0.000 0.000 0.000
#&gt; ERR519472     4  0.1608      0.854 0.000  0 0.000 0.928 0.072
#&gt; ERR519510     5  0.1908      0.876 0.000  0 0.000 0.092 0.908
#&gt; ERR519470     1  0.0000      0.952 1.000  0 0.000 0.000 0.000
#&gt; ERR519495     1  0.1331      0.943 0.952  0 0.000 0.040 0.008
#&gt; ERR519522     1  0.0000      0.952 1.000  0 0.000 0.000 0.000
#&gt; ERR519523     4  0.1197      0.863 0.000  0 0.000 0.952 0.048
#&gt; ERR519503     1  0.0000      0.952 1.000  0 0.000 0.000 0.000
#&gt; ERR519471     1  0.1408      0.941 0.948  0 0.000 0.044 0.008
#&gt; ERR519500     4  0.0963      0.867 0.000  0 0.000 0.964 0.036
#&gt; ERR519485     1  0.1697      0.933 0.932  0 0.000 0.060 0.008
#&gt; ERR519476     2  0.0000      1.000 0.000  1 0.000 0.000 0.000
#&gt; ERR519502     5  0.0290      0.866 0.000  0 0.000 0.008 0.992
#&gt; ERR519486     5  0.3953      0.769 0.148  0 0.000 0.060 0.792
#&gt; ERR519478     1  0.0000      0.952 1.000  0 0.000 0.000 0.000
#&gt; ERR519497     4  0.3424      0.696 0.000  0 0.000 0.760 0.240
#&gt; ERR519467     1  0.1410      0.920 0.940  0 0.000 0.060 0.000
#&gt; ERR519489     4  0.0290      0.861 0.000  0 0.000 0.992 0.008
#&gt; ERR519494     3  0.1608      0.900 0.000  0 0.928 0.000 0.072
#&gt; ERR519474     5  0.2439      0.864 0.004  0 0.000 0.120 0.876
#&gt; ERR519505     5  0.2773      0.817 0.000  0 0.164 0.000 0.836
#&gt; ERR519517     3  0.0000      0.938 0.000  0 1.000 0.000 0.000
#&gt; ERR519484     5  0.0290      0.866 0.000  0 0.000 0.008 0.992
#&gt; ERR519498     5  0.3109      0.795 0.000  0 0.200 0.000 0.800
#&gt; ERR519490     3  0.3053      0.797 0.000  0 0.828 0.008 0.164
#&gt; ERR519507     5  0.1908      0.876 0.000  0 0.000 0.092 0.908
#&gt; ERR519511     5  0.0404      0.867 0.000  0 0.000 0.012 0.988
#&gt; ERR519468     3  0.0000      0.938 0.000  0 1.000 0.000 0.000
#&gt; ERR519482     3  0.2193      0.877 0.000  0 0.900 0.008 0.092
#&gt; ERR519475     2  0.0000      1.000 0.000  1 0.000 0.000 0.000
#&gt; ERR519496     1  0.1251      0.944 0.956  0 0.000 0.036 0.008
#&gt; ERR519506     5  0.2505      0.872 0.020  0 0.000 0.092 0.888
#&gt; ERR519469     4  0.2233      0.851 0.004  0 0.000 0.892 0.104
#&gt; ERR519480     3  0.0000      0.938 0.000  0 1.000 0.000 0.000
#&gt; ERR519487     3  0.0000      0.938 0.000  0 1.000 0.000 0.000
#&gt; ERR519483     1  0.2563      0.877 0.872  0 0.000 0.120 0.008
#&gt; ERR519477     2  0.0000      1.000 0.000  1 0.000 0.000 0.000
#&gt; ERR519499     3  0.0000      0.938 0.000  0 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-4-a').click(function(){
  $('#tab-MAD-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-5'>
<p><a id='tab-MAD-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3    p4    p5    p6
#&gt; ERR519515     1  0.0000     0.9672 1.000  0 0.000 0.000 0.000 0.000
#&gt; ERR519516     1  0.3393     0.7589 0.784  0 0.000 0.192 0.020 0.004
#&gt; ERR519520     4  0.0260     0.8665 0.008  0 0.000 0.992 0.000 0.000
#&gt; ERR519513     5  0.2793     0.7451 0.000  0 0.200 0.000 0.800 0.000
#&gt; ERR519481     6  0.1075     0.8922 0.000  0 0.000 0.000 0.048 0.952
#&gt; ERR519491     1  0.0405     0.9655 0.988  0 0.000 0.008 0.000 0.004
#&gt; ERR519473     6  0.1556     0.9176 0.000  0 0.000 0.000 0.080 0.920
#&gt; ERR519518     4  0.3522     0.7500 0.000  0 0.000 0.800 0.128 0.072
#&gt; ERR519512     4  0.0000     0.8674 0.000  0 0.000 1.000 0.000 0.000
#&gt; ERR519521     4  0.0260     0.8675 0.000  0 0.000 0.992 0.000 0.008
#&gt; ERR519488     1  0.0146     0.9665 0.996  0 0.000 0.000 0.000 0.004
#&gt; ERR519493     5  0.2261     0.7652 0.104  0 0.000 0.008 0.884 0.004
#&gt; ERR519514     1  0.0000     0.9672 1.000  0 0.000 0.000 0.000 0.000
#&gt; ERR519479     5  0.0363     0.8272 0.000  0 0.000 0.000 0.988 0.012
#&gt; ERR519509     1  0.0146     0.9665 0.996  0 0.000 0.000 0.000 0.004
#&gt; ERR519472     6  0.1588     0.9156 0.004  0 0.000 0.000 0.072 0.924
#&gt; ERR519510     5  0.0260     0.8289 0.000  0 0.000 0.008 0.992 0.000
#&gt; ERR519470     1  0.0000     0.9672 1.000  0 0.000 0.000 0.000 0.000
#&gt; ERR519495     1  0.1584     0.9113 0.928  0 0.000 0.000 0.008 0.064
#&gt; ERR519522     1  0.0146     0.9665 0.996  0 0.000 0.000 0.000 0.004
#&gt; ERR519523     4  0.1226     0.8600 0.004  0 0.000 0.952 0.040 0.004
#&gt; ERR519503     1  0.0146     0.9665 0.996  0 0.000 0.000 0.000 0.004
#&gt; ERR519471     1  0.0405     0.9655 0.988  0 0.000 0.008 0.000 0.004
#&gt; ERR519500     4  0.1327     0.8535 0.000  0 0.000 0.936 0.000 0.064
#&gt; ERR519485     1  0.0405     0.9655 0.988  0 0.000 0.008 0.000 0.004
#&gt; ERR519476     2  0.0000     1.0000 0.000  1 0.000 0.000 0.000 0.000
#&gt; ERR519502     5  0.3607     0.4592 0.000  0 0.000 0.000 0.652 0.348
#&gt; ERR519486     5  0.3152     0.6822 0.196  0 0.000 0.008 0.792 0.004
#&gt; ERR519478     1  0.0000     0.9672 1.000  0 0.000 0.000 0.000 0.000
#&gt; ERR519497     4  0.4687     0.5285 0.000  0 0.000 0.624 0.308 0.068
#&gt; ERR519467     1  0.1863     0.8792 0.896  0 0.000 0.104 0.000 0.000
#&gt; ERR519489     4  0.1327     0.8535 0.000  0 0.000 0.936 0.000 0.064
#&gt; ERR519494     6  0.3707     0.7576 0.000  0 0.080 0.000 0.136 0.784
#&gt; ERR519474     5  0.0881     0.8288 0.008  0 0.000 0.008 0.972 0.012
#&gt; ERR519505     5  0.1663     0.8068 0.000  0 0.088 0.000 0.912 0.000
#&gt; ERR519517     3  0.0000     0.9000 0.000  0 1.000 0.000 0.000 0.000
#&gt; ERR519484     5  0.0000     0.8289 0.000  0 0.000 0.000 1.000 0.000
#&gt; ERR519498     5  0.2793     0.7451 0.000  0 0.200 0.000 0.800 0.000
#&gt; ERR519490     3  0.2980     0.8348 0.000  0 0.800 0.000 0.008 0.192
#&gt; ERR519507     5  0.3847     0.0922 0.000  0 0.000 0.000 0.544 0.456
#&gt; ERR519511     5  0.0000     0.8289 0.000  0 0.000 0.000 1.000 0.000
#&gt; ERR519468     3  0.2378     0.8646 0.000  0 0.848 0.000 0.000 0.152
#&gt; ERR519482     3  0.2730     0.8424 0.000  0 0.808 0.000 0.000 0.192
#&gt; ERR519475     2  0.0000     1.0000 0.000  1 0.000 0.000 0.000 0.000
#&gt; ERR519496     1  0.0405     0.9655 0.988  0 0.000 0.008 0.000 0.004
#&gt; ERR519506     5  0.1867     0.7968 0.020  0 0.000 0.000 0.916 0.064
#&gt; ERR519469     6  0.1644     0.9182 0.004  0 0.000 0.000 0.076 0.920
#&gt; ERR519480     3  0.0000     0.9000 0.000  0 1.000 0.000 0.000 0.000
#&gt; ERR519487     3  0.0000     0.9000 0.000  0 1.000 0.000 0.000 0.000
#&gt; ERR519483     1  0.0405     0.9655 0.988  0 0.000 0.008 0.000 0.004
#&gt; ERR519477     2  0.0000     1.0000 0.000  1 0.000 0.000 0.000 0.000
#&gt; ERR519499     3  0.0000     0.9000 0.000  0 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-5-a').click(function(){
  $('#tab-MAD-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-get-signatures'>
<ul>
<li><a href='#tab-MAD-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-1-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-1"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-2-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-2"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-3-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-3"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-4-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-4"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-5-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-pam-signature_compare](figure_cola/MAD-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-pam-collect-classes](figure_cola/MAD-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:mclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "mclust"]
# you can also extract it by
# res = res_list["MAD:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 18140 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-mclust-collect-plots](figure_cola/MAD-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-mclust-select-partition-number](figure_cola/MAD-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.998       0.999         0.1137 0.889   0.889
#> 3 3 0.322           0.473       0.733         3.3337 0.548   0.491
#> 4 4 0.603           0.790       0.866         0.3488 0.687   0.406
#> 5 5 0.546           0.644       0.779         0.0850 0.955   0.851
#> 6 6 0.581           0.478       0.746         0.0637 0.867   0.556
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-get-classes'>
<ul>
<li><a href='#tab-MAD-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-mclust-get-classes-1'>
<p><a id='tab-MAD-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; ERR519515     1  0.0000      0.999 1.000 0.000
#&gt; ERR519516     1  0.0000      0.999 1.000 0.000
#&gt; ERR519520     1  0.0000      0.999 1.000 0.000
#&gt; ERR519513     1  0.0000      0.999 1.000 0.000
#&gt; ERR519481     1  0.0000      0.999 1.000 0.000
#&gt; ERR519491     1  0.0000      0.999 1.000 0.000
#&gt; ERR519473     1  0.0000      0.999 1.000 0.000
#&gt; ERR519518     1  0.0000      0.999 1.000 0.000
#&gt; ERR519512     1  0.0000      0.999 1.000 0.000
#&gt; ERR519521     1  0.0000      0.999 1.000 0.000
#&gt; ERR519488     1  0.3114      0.941 0.944 0.056
#&gt; ERR519493     1  0.0000      0.999 1.000 0.000
#&gt; ERR519514     1  0.0000      0.999 1.000 0.000
#&gt; ERR519479     1  0.0000      0.999 1.000 0.000
#&gt; ERR519509     1  0.0376      0.995 0.996 0.004
#&gt; ERR519472     1  0.0000      0.999 1.000 0.000
#&gt; ERR519510     1  0.0000      0.999 1.000 0.000
#&gt; ERR519470     1  0.0000      0.999 1.000 0.000
#&gt; ERR519495     1  0.0000      0.999 1.000 0.000
#&gt; ERR519522     1  0.0000      0.999 1.000 0.000
#&gt; ERR519523     1  0.0000      0.999 1.000 0.000
#&gt; ERR519503     1  0.0000      0.999 1.000 0.000
#&gt; ERR519471     1  0.0000      0.999 1.000 0.000
#&gt; ERR519500     1  0.0000      0.999 1.000 0.000
#&gt; ERR519485     1  0.0000      0.999 1.000 0.000
#&gt; ERR519476     2  0.0000      1.000 0.000 1.000
#&gt; ERR519502     1  0.0000      0.999 1.000 0.000
#&gt; ERR519486     1  0.0000      0.999 1.000 0.000
#&gt; ERR519478     1  0.0000      0.999 1.000 0.000
#&gt; ERR519497     1  0.0000      0.999 1.000 0.000
#&gt; ERR519467     1  0.0000      0.999 1.000 0.000
#&gt; ERR519489     1  0.0000      0.999 1.000 0.000
#&gt; ERR519494     1  0.0000      0.999 1.000 0.000
#&gt; ERR519474     1  0.0000      0.999 1.000 0.000
#&gt; ERR519505     1  0.0000      0.999 1.000 0.000
#&gt; ERR519517     1  0.0000      0.999 1.000 0.000
#&gt; ERR519484     1  0.0000      0.999 1.000 0.000
#&gt; ERR519498     1  0.0000      0.999 1.000 0.000
#&gt; ERR519490     1  0.0000      0.999 1.000 0.000
#&gt; ERR519507     1  0.0000      0.999 1.000 0.000
#&gt; ERR519511     1  0.0000      0.999 1.000 0.000
#&gt; ERR519468     1  0.0000      0.999 1.000 0.000
#&gt; ERR519482     1  0.0000      0.999 1.000 0.000
#&gt; ERR519475     2  0.0000      1.000 0.000 1.000
#&gt; ERR519496     1  0.0000      0.999 1.000 0.000
#&gt; ERR519506     1  0.0000      0.999 1.000 0.000
#&gt; ERR519469     1  0.0000      0.999 1.000 0.000
#&gt; ERR519480     1  0.0000      0.999 1.000 0.000
#&gt; ERR519487     1  0.0000      0.999 1.000 0.000
#&gt; ERR519483     1  0.0000      0.999 1.000 0.000
#&gt; ERR519477     2  0.0000      1.000 0.000 1.000
#&gt; ERR519499     1  0.0000      0.999 1.000 0.000
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-1-a').click(function(){
  $('#tab-MAD-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-2'>
<p><a id='tab-MAD-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3
#&gt; ERR519515     1   0.141     0.6469 0.964  0 0.036
#&gt; ERR519516     1   0.304     0.6203 0.896  0 0.104
#&gt; ERR519520     3   0.565     0.5053 0.312  0 0.688
#&gt; ERR519513     3   0.000     0.6629 0.000  0 1.000
#&gt; ERR519481     3   0.630     0.1199 0.484  0 0.516
#&gt; ERR519491     1   0.141     0.6469 0.964  0 0.036
#&gt; ERR519473     3   0.630     0.1199 0.484  0 0.516
#&gt; ERR519518     3   0.412     0.6916 0.168  0 0.832
#&gt; ERR519512     3   0.460     0.6667 0.204  0 0.796
#&gt; ERR519521     3   0.418     0.6889 0.172  0 0.828
#&gt; ERR519488     1   0.312     0.6211 0.892  0 0.108
#&gt; ERR519493     1   0.141     0.6469 0.964  0 0.036
#&gt; ERR519514     1   0.141     0.6469 0.964  0 0.036
#&gt; ERR519479     1   0.630    -0.1257 0.520  0 0.480
#&gt; ERR519509     1   0.226     0.6394 0.932  0 0.068
#&gt; ERR519472     1   0.630    -0.1257 0.520  0 0.480
#&gt; ERR519510     1   0.630    -0.1069 0.528  0 0.472
#&gt; ERR519470     1   0.141     0.6469 0.964  0 0.036
#&gt; ERR519495     1   0.619     0.0163 0.580  0 0.420
#&gt; ERR519522     1   0.604     0.2344 0.620  0 0.380
#&gt; ERR519523     3   0.522     0.5998 0.260  0 0.740
#&gt; ERR519503     1   0.624     0.1207 0.560  0 0.440
#&gt; ERR519471     1   0.141     0.6469 0.964  0 0.036
#&gt; ERR519500     1   0.630    -0.1257 0.520  0 0.480
#&gt; ERR519485     1   0.141     0.6469 0.964  0 0.036
#&gt; ERR519476     2   0.000     1.0000 0.000  1 0.000
#&gt; ERR519502     3   0.630     0.1199 0.484  0 0.516
#&gt; ERR519486     1   0.312     0.6211 0.892  0 0.108
#&gt; ERR519478     1   0.141     0.6469 0.964  0 0.036
#&gt; ERR519497     3   0.412     0.6916 0.168  0 0.832
#&gt; ERR519467     1   0.597     0.2514 0.636  0 0.364
#&gt; ERR519489     3   0.590     0.4367 0.352  0 0.648
#&gt; ERR519494     3   0.236     0.7021 0.072  0 0.928
#&gt; ERR519474     1   0.597     0.1772 0.636  0 0.364
#&gt; ERR519505     3   0.312     0.6995 0.108  0 0.892
#&gt; ERR519517     3   0.000     0.6629 0.000  0 1.000
#&gt; ERR519484     3   0.631     0.1136 0.488  0 0.512
#&gt; ERR519498     3   0.288     0.6969 0.096  0 0.904
#&gt; ERR519490     3   0.236     0.7021 0.072  0 0.928
#&gt; ERR519507     1   0.630    -0.1257 0.520  0 0.480
#&gt; ERR519511     1   0.630    -0.1257 0.520  0 0.480
#&gt; ERR519468     3   0.236     0.7021 0.072  0 0.928
#&gt; ERR519482     3   0.236     0.7021 0.072  0 0.928
#&gt; ERR519475     2   0.000     1.0000 0.000  1 0.000
#&gt; ERR519496     1   0.319     0.6143 0.888  0 0.112
#&gt; ERR519506     3   0.630     0.1501 0.472  0 0.528
#&gt; ERR519469     3   0.412     0.6916 0.168  0 0.832
#&gt; ERR519480     3   0.000     0.6629 0.000  0 1.000
#&gt; ERR519487     3   0.000     0.6629 0.000  0 1.000
#&gt; ERR519483     3   0.631     0.1009 0.492  0 0.508
#&gt; ERR519477     2   0.000     1.0000 0.000  1 0.000
#&gt; ERR519499     3   0.000     0.6629 0.000  0 1.000
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-2-a').click(function(){
  $('#tab-MAD-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-3'>
<p><a id='tab-MAD-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3    p4
#&gt; ERR519515     1  0.0188      0.900 0.996  0 0.004 0.000
#&gt; ERR519516     1  0.1211      0.897 0.960  0 0.000 0.040
#&gt; ERR519520     1  0.5901      0.479 0.652  0 0.068 0.280
#&gt; ERR519513     3  0.1940      0.703 0.000  0 0.924 0.076
#&gt; ERR519481     4  0.1867      0.848 0.000  0 0.072 0.928
#&gt; ERR519491     1  0.0817      0.900 0.976  0 0.000 0.024
#&gt; ERR519473     4  0.2521      0.867 0.024  0 0.064 0.912
#&gt; ERR519518     4  0.4713      0.253 0.000  0 0.360 0.640
#&gt; ERR519512     4  0.5056      0.725 0.164  0 0.076 0.760
#&gt; ERR519521     4  0.3383      0.844 0.052  0 0.076 0.872
#&gt; ERR519488     1  0.2530      0.870 0.896  0 0.100 0.004
#&gt; ERR519493     1  0.1022      0.900 0.968  0 0.000 0.032
#&gt; ERR519514     1  0.0592      0.902 0.984  0 0.000 0.016
#&gt; ERR519479     4  0.0817      0.864 0.024  0 0.000 0.976
#&gt; ERR519509     1  0.2530      0.870 0.896  0 0.100 0.004
#&gt; ERR519472     4  0.0921      0.863 0.028  0 0.000 0.972
#&gt; ERR519510     4  0.2586      0.864 0.048  0 0.040 0.912
#&gt; ERR519470     1  0.1118      0.894 0.964  0 0.036 0.000
#&gt; ERR519495     4  0.2530      0.799 0.112  0 0.000 0.888
#&gt; ERR519522     1  0.2530      0.870 0.896  0 0.100 0.004
#&gt; ERR519523     4  0.4188      0.795 0.148  0 0.040 0.812
#&gt; ERR519503     1  0.2654      0.862 0.888  0 0.108 0.004
#&gt; ERR519471     1  0.0592      0.902 0.984  0 0.000 0.016
#&gt; ERR519500     4  0.1118      0.860 0.036  0 0.000 0.964
#&gt; ERR519485     1  0.0817      0.900 0.976  0 0.000 0.024
#&gt; ERR519476     2  0.0000      1.000 0.000  1 0.000 0.000
#&gt; ERR519502     4  0.1557      0.854 0.000  0 0.056 0.944
#&gt; ERR519486     1  0.1305      0.900 0.960  0 0.004 0.036
#&gt; ERR519478     1  0.1305      0.894 0.960  0 0.036 0.004
#&gt; ERR519497     4  0.3899      0.819 0.052  0 0.108 0.840
#&gt; ERR519467     1  0.0188      0.901 0.996  0 0.004 0.000
#&gt; ERR519489     4  0.1929      0.873 0.024  0 0.036 0.940
#&gt; ERR519494     3  0.4746      0.610 0.000  0 0.632 0.368
#&gt; ERR519474     4  0.2345      0.847 0.100  0 0.000 0.900
#&gt; ERR519505     3  0.7814      0.257 0.304  0 0.416 0.280
#&gt; ERR519517     3  0.2973      0.728 0.000  0 0.856 0.144
#&gt; ERR519484     4  0.1118      0.854 0.000  0 0.036 0.964
#&gt; ERR519498     3  0.6188      0.259 0.056  0 0.548 0.396
#&gt; ERR519490     3  0.4564      0.669 0.000  0 0.672 0.328
#&gt; ERR519507     4  0.1406      0.866 0.024  0 0.016 0.960
#&gt; ERR519511     4  0.1022      0.856 0.000  0 0.032 0.968
#&gt; ERR519468     3  0.4250      0.711 0.000  0 0.724 0.276
#&gt; ERR519482     3  0.4564      0.669 0.000  0 0.672 0.328
#&gt; ERR519475     2  0.0000      1.000 0.000  1 0.000 0.000
#&gt; ERR519496     1  0.4679      0.418 0.648  0 0.000 0.352
#&gt; ERR519506     4  0.3421      0.856 0.088  0 0.044 0.868
#&gt; ERR519469     4  0.3301      0.858 0.076  0 0.048 0.876
#&gt; ERR519480     3  0.2408      0.720 0.000  0 0.896 0.104
#&gt; ERR519487     3  0.1940      0.703 0.000  0 0.924 0.076
#&gt; ERR519483     4  0.4188      0.805 0.148  0 0.040 0.812
#&gt; ERR519477     2  0.0000      1.000 0.000  1 0.000 0.000
#&gt; ERR519499     3  0.1940      0.703 0.000  0 0.924 0.076
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-3-a').click(function(){
  $('#tab-MAD-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-4'>
<p><a id='tab-MAD-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3    p4    p5
#&gt; ERR519515     1  0.0162     0.7677 0.996  0 0.000 0.000 0.004
#&gt; ERR519516     1  0.1787     0.7629 0.936  0 0.004 0.044 0.016
#&gt; ERR519520     5  0.8385    -0.0935 0.172  0 0.212 0.260 0.356
#&gt; ERR519513     3  0.2648     0.6568 0.000  0 0.848 0.000 0.152
#&gt; ERR519481     4  0.5067     0.7231 0.000  0 0.128 0.700 0.172
#&gt; ERR519491     1  0.0510     0.7748 0.984  0 0.000 0.016 0.000
#&gt; ERR519473     4  0.5456     0.7409 0.028  0 0.120 0.708 0.144
#&gt; ERR519518     4  0.6673     0.1681 0.000  0 0.316 0.432 0.252
#&gt; ERR519512     4  0.7270     0.5924 0.080  0 0.192 0.536 0.192
#&gt; ERR519521     4  0.5814     0.6741 0.008  0 0.176 0.640 0.176
#&gt; ERR519488     5  0.3916     0.6770 0.256  0 0.000 0.012 0.732
#&gt; ERR519493     1  0.1774     0.7600 0.932  0 0.000 0.052 0.016
#&gt; ERR519514     1  0.0404     0.7727 0.988  0 0.000 0.012 0.000
#&gt; ERR519479     4  0.1485     0.7161 0.032  0 0.000 0.948 0.020
#&gt; ERR519509     5  0.4040     0.6516 0.276  0 0.000 0.012 0.712
#&gt; ERR519472     4  0.1648     0.7154 0.040  0 0.000 0.940 0.020
#&gt; ERR519510     4  0.3067     0.7049 0.012  0 0.140 0.844 0.004
#&gt; ERR519470     1  0.2424     0.6669 0.868  0 0.000 0.000 0.132
#&gt; ERR519495     4  0.2130     0.7058 0.080  0 0.000 0.908 0.012
#&gt; ERR519522     5  0.3863     0.6777 0.248  0 0.000 0.012 0.740
#&gt; ERR519523     4  0.5794     0.7248 0.096  0 0.052 0.688 0.164
#&gt; ERR519503     5  0.5355     0.5832 0.316  0 0.044 0.016 0.624
#&gt; ERR519471     1  0.0566     0.7733 0.984  0 0.000 0.012 0.004
#&gt; ERR519500     4  0.2409     0.7139 0.056  0 0.008 0.908 0.028
#&gt; ERR519485     1  0.0609     0.7749 0.980  0 0.000 0.020 0.000
#&gt; ERR519476     2  0.0000     1.0000 0.000  1 0.000 0.000 0.000
#&gt; ERR519502     4  0.4922     0.7196 0.000  0 0.128 0.716 0.156
#&gt; ERR519486     1  0.5719     0.2738 0.596  0 0.000 0.284 0.120
#&gt; ERR519478     1  0.2179     0.6961 0.888  0 0.000 0.000 0.112
#&gt; ERR519497     4  0.6191     0.5649 0.004  0 0.252 0.568 0.176
#&gt; ERR519467     1  0.5854     0.2166 0.596  0 0.000 0.152 0.252
#&gt; ERR519489     4  0.5592     0.7408 0.048  0 0.088 0.704 0.160
#&gt; ERR519494     3  0.6571     0.4104 0.000  0 0.472 0.268 0.260
#&gt; ERR519474     4  0.2248     0.7067 0.088  0 0.000 0.900 0.012
#&gt; ERR519505     3  0.6795     0.2558 0.012  0 0.488 0.224 0.276
#&gt; ERR519517     3  0.1205     0.6662 0.000  0 0.956 0.040 0.004
#&gt; ERR519484     4  0.4233     0.7388 0.008  0 0.084 0.792 0.116
#&gt; ERR519498     3  0.6228     0.3261 0.004  0 0.568 0.228 0.200
#&gt; ERR519490     3  0.6120     0.5406 0.000  0 0.564 0.240 0.196
#&gt; ERR519507     4  0.1967     0.7190 0.036  0 0.012 0.932 0.020
#&gt; ERR519511     4  0.2899     0.7259 0.008  0 0.076 0.880 0.036
#&gt; ERR519468     3  0.4334     0.6548 0.000  0 0.768 0.140 0.092
#&gt; ERR519482     3  0.5911     0.5707 0.000  0 0.596 0.228 0.176
#&gt; ERR519475     2  0.0000     1.0000 0.000  1 0.000 0.000 0.000
#&gt; ERR519496     1  0.4268     0.3472 0.648  0 0.000 0.344 0.008
#&gt; ERR519506     4  0.4892     0.7574 0.052  0 0.052 0.760 0.136
#&gt; ERR519469     4  0.4385     0.7528 0.020  0 0.044 0.776 0.160
#&gt; ERR519480     3  0.1386     0.6723 0.000  0 0.952 0.016 0.032
#&gt; ERR519487     3  0.0609     0.6396 0.000  0 0.980 0.000 0.020
#&gt; ERR519483     4  0.5348     0.7420 0.096  0 0.044 0.728 0.132
#&gt; ERR519477     2  0.0000     1.0000 0.000  1 0.000 0.000 0.000
#&gt; ERR519499     3  0.0609     0.6396 0.000  0 0.980 0.000 0.020
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-4-a').click(function(){
  $('#tab-MAD-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-5'>
<p><a id='tab-MAD-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3    p4    p5    p6
#&gt; ERR519515     1  0.0000     0.8519 1.000  0 0.000 0.000 0.000 0.000
#&gt; ERR519516     1  0.1370     0.8462 0.948  0 0.004 0.000 0.036 0.012
#&gt; ERR519520     4  0.7068     0.1684 0.040  0 0.048 0.504 0.224 0.184
#&gt; ERR519513     4  0.1867    -0.0504 0.000  0 0.064 0.916 0.000 0.020
#&gt; ERR519481     5  0.6194     0.3277 0.020  0 0.188 0.316 0.476 0.000
#&gt; ERR519491     1  0.0260     0.8537 0.992  0 0.000 0.000 0.008 0.000
#&gt; ERR519473     5  0.4093     0.4681 0.008  0 0.012 0.324 0.656 0.000
#&gt; ERR519518     4  0.6054     0.0841 0.000  0 0.236 0.484 0.272 0.008
#&gt; ERR519512     4  0.6920     0.0958 0.040  0 0.088 0.500 0.300 0.072
#&gt; ERR519521     4  0.6028    -0.0251 0.032  0 0.092 0.508 0.360 0.008
#&gt; ERR519488     6  0.1686     0.8444 0.064  0 0.000 0.012 0.000 0.924
#&gt; ERR519493     1  0.1010     0.8474 0.960  0 0.000 0.000 0.036 0.004
#&gt; ERR519514     1  0.0146     0.8529 0.996  0 0.000 0.000 0.004 0.000
#&gt; ERR519479     5  0.0260     0.6298 0.008  0 0.000 0.000 0.992 0.000
#&gt; ERR519509     6  0.1501     0.8365 0.076  0 0.000 0.000 0.000 0.924
#&gt; ERR519472     5  0.0260     0.6298 0.008  0 0.000 0.000 0.992 0.000
#&gt; ERR519510     5  0.5058     0.4716 0.020  0 0.092 0.176 0.700 0.012
#&gt; ERR519470     1  0.2562     0.7409 0.828  0 0.000 0.000 0.000 0.172
#&gt; ERR519495     5  0.0547     0.6306 0.020  0 0.000 0.000 0.980 0.000
#&gt; ERR519522     6  0.1983     0.8430 0.072  0 0.000 0.020 0.000 0.908
#&gt; ERR519523     4  0.7113    -0.1610 0.164  0 0.072 0.384 0.368 0.012
#&gt; ERR519503     6  0.4871     0.5462 0.132  0 0.000 0.212 0.000 0.656
#&gt; ERR519471     1  0.0291     0.8525 0.992  0 0.000 0.004 0.004 0.000
#&gt; ERR519500     5  0.2313     0.6007 0.100  0 0.012 0.000 0.884 0.004
#&gt; ERR519485     1  0.0520     0.8513 0.984  0 0.000 0.000 0.008 0.008
#&gt; ERR519476     2  0.0000     1.0000 0.000  1 0.000 0.000 0.000 0.000
#&gt; ERR519502     5  0.6263     0.2439 0.012  0 0.236 0.324 0.428 0.000
#&gt; ERR519486     1  0.5189     0.5122 0.676  0 0.000 0.072 0.200 0.052
#&gt; ERR519478     1  0.2482     0.7663 0.848  0 0.000 0.000 0.004 0.148
#&gt; ERR519497     4  0.6023     0.1264 0.000  0 0.092 0.548 0.300 0.060
#&gt; ERR519467     1  0.5675     0.5055 0.640  0 0.000 0.096 0.072 0.192
#&gt; ERR519489     4  0.6388    -0.2302 0.096  0 0.060 0.420 0.420 0.004
#&gt; ERR519494     3  0.3464     0.5866 0.000  0 0.688 0.312 0.000 0.000
#&gt; ERR519474     5  0.1036     0.6293 0.024  0 0.000 0.004 0.964 0.008
#&gt; ERR519505     4  0.3595     0.2473 0.000  0 0.000 0.796 0.120 0.084
#&gt; ERR519517     4  0.4812    -0.1252 0.000  0 0.344 0.588 0.000 0.068
#&gt; ERR519484     5  0.5461     0.4592 0.004  0 0.196 0.208 0.592 0.000
#&gt; ERR519498     4  0.3332     0.2657 0.000  0 0.000 0.808 0.144 0.048
#&gt; ERR519490     3  0.4311     0.6344 0.004  0 0.708 0.228 0.060 0.000
#&gt; ERR519507     5  0.0653     0.6330 0.012  0 0.004 0.004 0.980 0.000
#&gt; ERR519511     5  0.3560     0.5888 0.064  0 0.040 0.056 0.836 0.004
#&gt; ERR519468     3  0.5040     0.2588 0.000  0 0.552 0.380 0.008 0.060
#&gt; ERR519482     3  0.2793     0.6566 0.000  0 0.800 0.200 0.000 0.000
#&gt; ERR519475     2  0.0000     1.0000 0.000  1 0.000 0.000 0.000 0.000
#&gt; ERR519496     1  0.2894     0.7532 0.852  0 0.000 0.036 0.108 0.004
#&gt; ERR519506     5  0.4580     0.3953 0.028  0 0.004 0.368 0.596 0.004
#&gt; ERR519469     5  0.4868     0.3229 0.004  0 0.044 0.384 0.564 0.004
#&gt; ERR519480     4  0.4515    -0.2214 0.000  0 0.304 0.640 0.000 0.056
#&gt; ERR519487     4  0.4718    -0.1042 0.000  0 0.316 0.616 0.000 0.068
#&gt; ERR519483     5  0.4647     0.3929 0.032  0 0.004 0.368 0.592 0.004
#&gt; ERR519477     2  0.0000     1.0000 0.000  1 0.000 0.000 0.000 0.000
#&gt; ERR519499     4  0.4718    -0.1042 0.000  0 0.316 0.616 0.000 0.068
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-5-a').click(function(){
  $('#tab-MAD-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-get-signatures'>
<ul>
<li><a href='#tab-MAD-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-1-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-1"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-2-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-2"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-3-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-3"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-4-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-4"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-5-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-mclust-signature_compare](figure_cola/MAD-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-mclust-collect-classes](figure_cola/MAD-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:NMF






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "NMF"]
# you can also extract it by
# res = res_list["MAD:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 18140 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-NMF-collect-plots](figure_cola/MAD-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-NMF-select-partition-number](figure_cola/MAD-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.737           0.884       0.951         0.5050 0.491   0.491
#> 3 3 0.528           0.764       0.867         0.3154 0.718   0.487
#> 4 4 0.576           0.657       0.812         0.1295 0.835   0.551
#> 5 5 0.592           0.563       0.761         0.0598 0.897   0.625
#> 6 6 0.650           0.551       0.747         0.0341 0.931   0.694
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-get-classes'>
<ul>
<li><a href='#tab-MAD-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-NMF-get-classes-1'>
<p><a id='tab-MAD-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; ERR519515     2  0.0000     0.9607 0.000 1.000
#&gt; ERR519516     2  0.0376     0.9576 0.004 0.996
#&gt; ERR519520     2  0.0000     0.9607 0.000 1.000
#&gt; ERR519513     1  0.0000     0.9293 1.000 0.000
#&gt; ERR519481     1  0.0000     0.9293 1.000 0.000
#&gt; ERR519491     2  0.0000     0.9607 0.000 1.000
#&gt; ERR519473     1  0.0000     0.9293 1.000 0.000
#&gt; ERR519518     1  0.0000     0.9293 1.000 0.000
#&gt; ERR519512     2  0.0000     0.9607 0.000 1.000
#&gt; ERR519521     1  0.7883     0.7212 0.764 0.236
#&gt; ERR519488     2  0.0000     0.9607 0.000 1.000
#&gt; ERR519493     2  0.0000     0.9607 0.000 1.000
#&gt; ERR519514     2  0.0000     0.9607 0.000 1.000
#&gt; ERR519479     2  0.9963     0.0348 0.464 0.536
#&gt; ERR519509     2  0.0000     0.9607 0.000 1.000
#&gt; ERR519472     1  0.5946     0.8305 0.856 0.144
#&gt; ERR519510     1  0.9896     0.2606 0.560 0.440
#&gt; ERR519470     2  0.0000     0.9607 0.000 1.000
#&gt; ERR519495     2  0.0000     0.9607 0.000 1.000
#&gt; ERR519522     2  0.0000     0.9607 0.000 1.000
#&gt; ERR519523     2  0.0000     0.9607 0.000 1.000
#&gt; ERR519503     2  0.0000     0.9607 0.000 1.000
#&gt; ERR519471     2  0.0000     0.9607 0.000 1.000
#&gt; ERR519500     2  0.8955     0.4868 0.312 0.688
#&gt; ERR519485     2  0.0000     0.9607 0.000 1.000
#&gt; ERR519476     2  0.0000     0.9607 0.000 1.000
#&gt; ERR519502     1  0.0000     0.9293 1.000 0.000
#&gt; ERR519486     2  0.0000     0.9607 0.000 1.000
#&gt; ERR519478     2  0.0000     0.9607 0.000 1.000
#&gt; ERR519497     1  0.0000     0.9293 1.000 0.000
#&gt; ERR519467     2  0.0000     0.9607 0.000 1.000
#&gt; ERR519489     1  0.5519     0.8345 0.872 0.128
#&gt; ERR519494     1  0.0000     0.9293 1.000 0.000
#&gt; ERR519474     2  0.0376     0.9576 0.004 0.996
#&gt; ERR519505     1  0.0000     0.9293 1.000 0.000
#&gt; ERR519517     1  0.0000     0.9293 1.000 0.000
#&gt; ERR519484     1  0.0000     0.9293 1.000 0.000
#&gt; ERR519498     1  0.0000     0.9293 1.000 0.000
#&gt; ERR519490     1  0.0000     0.9293 1.000 0.000
#&gt; ERR519507     1  0.6438     0.8102 0.836 0.164
#&gt; ERR519511     1  0.7674     0.7386 0.776 0.224
#&gt; ERR519468     1  0.0000     0.9293 1.000 0.000
#&gt; ERR519482     1  0.0000     0.9293 1.000 0.000
#&gt; ERR519475     2  0.3274     0.9022 0.060 0.940
#&gt; ERR519496     2  0.0000     0.9607 0.000 1.000
#&gt; ERR519506     1  0.0000     0.9293 1.000 0.000
#&gt; ERR519469     1  0.0000     0.9293 1.000 0.000
#&gt; ERR519480     1  0.0000     0.9293 1.000 0.000
#&gt; ERR519487     1  0.0000     0.9293 1.000 0.000
#&gt; ERR519483     1  0.6801     0.7779 0.820 0.180
#&gt; ERR519477     1  0.7139     0.7758 0.804 0.196
#&gt; ERR519499     1  0.0000     0.9293 1.000 0.000
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-1-a').click(function(){
  $('#tab-MAD-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-2'>
<p><a id='tab-MAD-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; ERR519515     2  0.1860      0.854 0.052 0.948 0.000
#&gt; ERR519516     1  0.6724      0.131 0.568 0.420 0.012
#&gt; ERR519520     2  0.2165      0.827 0.000 0.936 0.064
#&gt; ERR519513     3  0.2356      0.878 0.072 0.000 0.928
#&gt; ERR519481     1  0.1860      0.827 0.948 0.000 0.052
#&gt; ERR519491     2  0.5678      0.617 0.316 0.684 0.000
#&gt; ERR519473     1  0.1411      0.836 0.964 0.000 0.036
#&gt; ERR519518     3  0.3879      0.846 0.152 0.000 0.848
#&gt; ERR519512     2  0.1411      0.840 0.000 0.964 0.036
#&gt; ERR519521     1  0.4099      0.780 0.852 0.008 0.140
#&gt; ERR519488     2  0.0592      0.848 0.000 0.988 0.012
#&gt; ERR519493     2  0.6095      0.459 0.392 0.608 0.000
#&gt; ERR519514     2  0.3038      0.839 0.104 0.896 0.000
#&gt; ERR519479     1  0.1182      0.843 0.976 0.012 0.012
#&gt; ERR519509     2  0.0237      0.850 0.000 0.996 0.004
#&gt; ERR519472     1  0.1163      0.838 0.972 0.028 0.000
#&gt; ERR519510     1  0.6420      0.568 0.688 0.024 0.288
#&gt; ERR519470     2  0.1529      0.855 0.040 0.960 0.000
#&gt; ERR519495     1  0.3038      0.790 0.896 0.104 0.000
#&gt; ERR519522     2  0.0892      0.855 0.020 0.980 0.000
#&gt; ERR519523     2  0.5760      0.592 0.328 0.672 0.000
#&gt; ERR519503     2  0.4002      0.751 0.000 0.840 0.160
#&gt; ERR519471     2  0.3482      0.828 0.128 0.872 0.000
#&gt; ERR519500     1  0.2096      0.833 0.944 0.052 0.004
#&gt; ERR519485     1  0.6308     -0.166 0.508 0.492 0.000
#&gt; ERR519476     2  0.6389      0.752 0.124 0.768 0.108
#&gt; ERR519502     1  0.4002      0.750 0.840 0.000 0.160
#&gt; ERR519486     2  0.3340      0.835 0.120 0.880 0.000
#&gt; ERR519478     2  0.1031      0.855 0.024 0.976 0.000
#&gt; ERR519497     3  0.1031      0.873 0.024 0.000 0.976
#&gt; ERR519467     2  0.1163      0.856 0.028 0.972 0.000
#&gt; ERR519489     1  0.2804      0.831 0.924 0.016 0.060
#&gt; ERR519494     3  0.5905      0.611 0.352 0.000 0.648
#&gt; ERR519474     1  0.3412      0.770 0.876 0.124 0.000
#&gt; ERR519505     3  0.2301      0.831 0.004 0.060 0.936
#&gt; ERR519517     3  0.1643      0.880 0.044 0.000 0.956
#&gt; ERR519484     1  0.2066      0.825 0.940 0.000 0.060
#&gt; ERR519498     3  0.1453      0.852 0.008 0.024 0.968
#&gt; ERR519490     3  0.5098      0.768 0.248 0.000 0.752
#&gt; ERR519507     1  0.1015      0.842 0.980 0.008 0.012
#&gt; ERR519511     1  0.2945      0.811 0.908 0.004 0.088
#&gt; ERR519468     3  0.3941      0.845 0.156 0.000 0.844
#&gt; ERR519482     3  0.4931      0.786 0.232 0.000 0.768
#&gt; ERR519475     2  0.8030      0.624 0.144 0.652 0.204
#&gt; ERR519496     2  0.4504      0.775 0.196 0.804 0.000
#&gt; ERR519506     1  0.1315      0.840 0.972 0.008 0.020
#&gt; ERR519469     1  0.3989      0.761 0.864 0.012 0.124
#&gt; ERR519480     3  0.2066      0.879 0.060 0.000 0.940
#&gt; ERR519487     3  0.1289      0.878 0.032 0.000 0.968
#&gt; ERR519483     1  0.3263      0.828 0.912 0.048 0.040
#&gt; ERR519477     3  0.7104      0.668 0.140 0.136 0.724
#&gt; ERR519499     3  0.1289      0.878 0.032 0.000 0.968
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-2-a').click(function(){
  $('#tab-MAD-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-3'>
<p><a id='tab-MAD-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; ERR519515     1  0.1174     0.8551 0.968 0.012 0.000 0.020
#&gt; ERR519516     2  0.5954     0.2960 0.052 0.604 0.000 0.344
#&gt; ERR519520     1  0.3764     0.7567 0.816 0.172 0.012 0.000
#&gt; ERR519513     2  0.4697     0.3581 0.000 0.644 0.356 0.000
#&gt; ERR519481     4  0.3547     0.7193 0.000 0.144 0.016 0.840
#&gt; ERR519491     1  0.5650     0.6316 0.716 0.180 0.000 0.104
#&gt; ERR519473     4  0.1151     0.7776 0.000 0.008 0.024 0.968
#&gt; ERR519518     3  0.2546     0.7997 0.000 0.028 0.912 0.060
#&gt; ERR519512     1  0.4034     0.7537 0.796 0.192 0.004 0.008
#&gt; ERR519521     4  0.5509     0.2770 0.004 0.424 0.012 0.560
#&gt; ERR519488     1  0.1576     0.8409 0.948 0.048 0.004 0.000
#&gt; ERR519493     2  0.4656     0.6320 0.072 0.792 0.000 0.136
#&gt; ERR519514     1  0.1406     0.8543 0.960 0.016 0.000 0.024
#&gt; ERR519479     4  0.4098     0.6583 0.012 0.204 0.000 0.784
#&gt; ERR519509     1  0.1022     0.8491 0.968 0.032 0.000 0.000
#&gt; ERR519472     4  0.1042     0.7863 0.008 0.020 0.000 0.972
#&gt; ERR519510     2  0.2676     0.6379 0.000 0.896 0.092 0.012
#&gt; ERR519470     1  0.1174     0.8551 0.968 0.012 0.000 0.020
#&gt; ERR519495     4  0.4592     0.7315 0.128 0.064 0.004 0.804
#&gt; ERR519522     1  0.0895     0.8548 0.976 0.020 0.000 0.004
#&gt; ERR519523     1  0.5576     0.6471 0.720 0.096 0.000 0.184
#&gt; ERR519503     1  0.2363     0.8271 0.920 0.024 0.056 0.000
#&gt; ERR519471     1  0.1356     0.8535 0.960 0.008 0.000 0.032
#&gt; ERR519500     4  0.1229     0.7836 0.004 0.020 0.008 0.968
#&gt; ERR519485     1  0.5540     0.6451 0.720 0.068 0.004 0.208
#&gt; ERR519476     1  0.8230     0.0704 0.428 0.372 0.032 0.168
#&gt; ERR519502     2  0.4353     0.6052 0.000 0.756 0.012 0.232
#&gt; ERR519486     2  0.5359     0.4845 0.288 0.680 0.004 0.028
#&gt; ERR519478     1  0.0524     0.8561 0.988 0.004 0.000 0.008
#&gt; ERR519497     3  0.5407     0.1376 0.012 0.484 0.504 0.000
#&gt; ERR519467     1  0.0927     0.8558 0.976 0.016 0.000 0.008
#&gt; ERR519489     4  0.3436     0.7296 0.008 0.016 0.112 0.864
#&gt; ERR519494     3  0.3577     0.7410 0.000 0.012 0.832 0.156
#&gt; ERR519474     4  0.3959     0.7512 0.092 0.068 0.000 0.840
#&gt; ERR519505     2  0.3610     0.5635 0.000 0.800 0.200 0.000
#&gt; ERR519517     3  0.0657     0.8097 0.000 0.004 0.984 0.012
#&gt; ERR519484     2  0.5073     0.6204 0.000 0.744 0.056 0.200
#&gt; ERR519498     2  0.4103     0.5140 0.000 0.744 0.256 0.000
#&gt; ERR519490     3  0.4295     0.6638 0.000 0.008 0.752 0.240
#&gt; ERR519507     4  0.2940     0.7722 0.008 0.088 0.012 0.892
#&gt; ERR519511     2  0.5835     0.3752 0.000 0.588 0.040 0.372
#&gt; ERR519468     3  0.0817     0.8106 0.000 0.000 0.976 0.024
#&gt; ERR519482     3  0.2589     0.7800 0.000 0.000 0.884 0.116
#&gt; ERR519475     2  0.8857     0.0404 0.356 0.408 0.084 0.152
#&gt; ERR519496     1  0.2246     0.8419 0.928 0.016 0.004 0.052
#&gt; ERR519506     4  0.3562     0.7596 0.084 0.016 0.028 0.872
#&gt; ERR519469     4  0.6094     0.6200 0.084 0.012 0.212 0.692
#&gt; ERR519480     3  0.0469     0.8075 0.000 0.012 0.988 0.000
#&gt; ERR519487     3  0.1118     0.7986 0.000 0.036 0.964 0.000
#&gt; ERR519483     4  0.6358     0.6270 0.164 0.020 0.120 0.696
#&gt; ERR519477     3  0.8075     0.0309 0.048 0.412 0.428 0.112
#&gt; ERR519499     3  0.0336     0.8080 0.000 0.008 0.992 0.000
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-3-a').click(function(){
  $('#tab-MAD-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-4'>
<p><a id='tab-MAD-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; ERR519515     1  0.0771     0.7823 0.976 0.020 0.000 0.000 0.004
#&gt; ERR519516     5  0.7833    -0.0477 0.068 0.244 0.000 0.332 0.356
#&gt; ERR519520     1  0.5094     0.4145 0.616 0.344 0.004 0.004 0.032
#&gt; ERR519513     5  0.3242     0.5891 0.000 0.012 0.172 0.000 0.816
#&gt; ERR519481     4  0.2102     0.6482 0.000 0.004 0.012 0.916 0.068
#&gt; ERR519491     1  0.4277     0.6379 0.808 0.044 0.000 0.052 0.096
#&gt; ERR519473     4  0.1377     0.6470 0.000 0.020 0.020 0.956 0.004
#&gt; ERR519518     3  0.3441     0.8508 0.000 0.004 0.828 0.140 0.028
#&gt; ERR519512     1  0.5759     0.3824 0.588 0.328 0.000 0.016 0.068
#&gt; ERR519521     4  0.5965     0.4346 0.004 0.220 0.004 0.620 0.152
#&gt; ERR519488     1  0.1892     0.7661 0.916 0.080 0.004 0.000 0.000
#&gt; ERR519493     5  0.3309     0.5841 0.052 0.032 0.000 0.048 0.868
#&gt; ERR519514     1  0.1560     0.7731 0.948 0.028 0.000 0.020 0.004
#&gt; ERR519479     4  0.6186     0.3957 0.004 0.148 0.000 0.548 0.300
#&gt; ERR519509     1  0.1341     0.7805 0.944 0.056 0.000 0.000 0.000
#&gt; ERR519472     4  0.1408     0.6465 0.000 0.044 0.000 0.948 0.008
#&gt; ERR519510     5  0.1220     0.6202 0.004 0.020 0.004 0.008 0.964
#&gt; ERR519470     1  0.0703     0.7811 0.976 0.024 0.000 0.000 0.000
#&gt; ERR519495     4  0.6638     0.1523 0.284 0.128 0.000 0.552 0.036
#&gt; ERR519522     1  0.0880     0.7884 0.968 0.032 0.000 0.000 0.000
#&gt; ERR519523     1  0.3497     0.6838 0.840 0.008 0.000 0.108 0.044
#&gt; ERR519503     1  0.3427     0.6861 0.836 0.056 0.108 0.000 0.000
#&gt; ERR519471     1  0.3282     0.5962 0.804 0.188 0.000 0.008 0.000
#&gt; ERR519500     4  0.0566     0.6512 0.000 0.000 0.012 0.984 0.004
#&gt; ERR519485     2  0.5039     0.4996 0.360 0.604 0.000 0.008 0.028
#&gt; ERR519476     2  0.8175     0.2244 0.328 0.396 0.012 0.108 0.156
#&gt; ERR519502     4  0.4804     0.1110 0.000 0.008 0.008 0.524 0.460
#&gt; ERR519486     5  0.6654    -0.2408 0.172 0.384 0.000 0.008 0.436
#&gt; ERR519478     1  0.0451     0.7885 0.988 0.008 0.000 0.000 0.004
#&gt; ERR519497     5  0.7037     0.2698 0.004 0.296 0.300 0.004 0.396
#&gt; ERR519467     1  0.1124     0.7899 0.960 0.036 0.000 0.004 0.000
#&gt; ERR519489     4  0.3497     0.5949 0.000 0.044 0.108 0.840 0.008
#&gt; ERR519494     3  0.4583     0.7906 0.000 0.008 0.764 0.128 0.100
#&gt; ERR519474     2  0.6752     0.3363 0.136 0.556 0.000 0.264 0.044
#&gt; ERR519505     5  0.2719     0.6230 0.000 0.068 0.048 0.000 0.884
#&gt; ERR519517     3  0.0671     0.8943 0.000 0.016 0.980 0.000 0.004
#&gt; ERR519484     5  0.2452     0.6095 0.000 0.052 0.028 0.012 0.908
#&gt; ERR519498     5  0.3362     0.6187 0.000 0.076 0.080 0.000 0.844
#&gt; ERR519490     3  0.2964     0.8482 0.000 0.004 0.840 0.152 0.004
#&gt; ERR519507     4  0.6288     0.3170 0.000 0.304 0.000 0.516 0.180
#&gt; ERR519511     5  0.4471     0.2990 0.004 0.020 0.000 0.292 0.684
#&gt; ERR519468     3  0.0451     0.8964 0.000 0.000 0.988 0.008 0.004
#&gt; ERR519482     3  0.2488     0.8701 0.000 0.000 0.872 0.124 0.004
#&gt; ERR519475     2  0.9079     0.2077 0.244 0.388 0.072 0.120 0.176
#&gt; ERR519496     1  0.3671     0.4928 0.756 0.236 0.000 0.008 0.000
#&gt; ERR519506     2  0.6867     0.4942 0.152 0.632 0.028 0.056 0.132
#&gt; ERR519469     4  0.7275     0.3026 0.156 0.072 0.208 0.556 0.008
#&gt; ERR519480     3  0.1907     0.8697 0.000 0.028 0.928 0.000 0.044
#&gt; ERR519487     3  0.1357     0.8791 0.000 0.004 0.948 0.000 0.048
#&gt; ERR519483     2  0.4913     0.5036 0.352 0.620 0.016 0.008 0.004
#&gt; ERR519477     5  0.8556     0.2577 0.036 0.180 0.284 0.096 0.404
#&gt; ERR519499     3  0.0671     0.8939 0.000 0.016 0.980 0.000 0.004
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-4-a').click(function(){
  $('#tab-MAD-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-5'>
<p><a id='tab-MAD-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; ERR519515     1  0.1155     0.7976 0.956 0.004 0.000 0.000 0.004 0.036
#&gt; ERR519516     5  0.6162     0.3992 0.060 0.104 0.000 0.308 0.528 0.000
#&gt; ERR519520     1  0.5031     0.4037 0.600 0.332 0.012 0.052 0.004 0.000
#&gt; ERR519513     4  0.4745     0.4591 0.000 0.056 0.248 0.676 0.000 0.020
#&gt; ERR519481     5  0.2244     0.6460 0.000 0.004 0.004 0.100 0.888 0.004
#&gt; ERR519491     1  0.4483     0.6851 0.780 0.016 0.000 0.072 0.048 0.084
#&gt; ERR519473     5  0.1922     0.6324 0.000 0.012 0.040 0.000 0.924 0.024
#&gt; ERR519518     3  0.5687     0.5721 0.000 0.136 0.608 0.012 0.232 0.012
#&gt; ERR519512     1  0.6830     0.0925 0.452 0.352 0.016 0.076 0.104 0.000
#&gt; ERR519521     5  0.4605     0.5870 0.012 0.096 0.008 0.148 0.736 0.000
#&gt; ERR519488     1  0.1226     0.7883 0.952 0.040 0.004 0.000 0.000 0.004
#&gt; ERR519493     4  0.4797     0.5046 0.096 0.024 0.000 0.760 0.068 0.052
#&gt; ERR519514     1  0.1586     0.7952 0.940 0.012 0.000 0.004 0.004 0.040
#&gt; ERR519479     5  0.6546     0.1565 0.008 0.020 0.000 0.348 0.420 0.204
#&gt; ERR519509     1  0.0858     0.7956 0.968 0.028 0.004 0.000 0.000 0.000
#&gt; ERR519472     5  0.2113     0.6266 0.000 0.008 0.000 0.004 0.896 0.092
#&gt; ERR519510     4  0.1294     0.6294 0.000 0.008 0.004 0.956 0.008 0.024
#&gt; ERR519470     1  0.1155     0.7976 0.956 0.004 0.000 0.000 0.004 0.036
#&gt; ERR519495     5  0.7357    -0.0103 0.348 0.044 0.000 0.040 0.376 0.192
#&gt; ERR519522     1  0.0291     0.7997 0.992 0.004 0.004 0.000 0.000 0.000
#&gt; ERR519523     1  0.2873     0.7554 0.872 0.004 0.000 0.044 0.068 0.012
#&gt; ERR519503     1  0.5180     0.5542 0.684 0.180 0.088 0.000 0.000 0.048
#&gt; ERR519471     1  0.4184     0.4463 0.640 0.012 0.004 0.000 0.004 0.340
#&gt; ERR519500     5  0.1498     0.6350 0.004 0.024 0.012 0.000 0.948 0.012
#&gt; ERR519485     6  0.2871     0.6820 0.100 0.012 0.000 0.016 0.008 0.864
#&gt; ERR519476     2  0.7916     0.3746 0.200 0.472 0.004 0.116 0.096 0.112
#&gt; ERR519502     5  0.4332     0.4628 0.000 0.020 0.008 0.344 0.628 0.000
#&gt; ERR519486     6  0.6115     0.3822 0.116 0.032 0.008 0.308 0.000 0.536
#&gt; ERR519478     1  0.0767     0.8010 0.976 0.012 0.000 0.004 0.000 0.008
#&gt; ERR519497     2  0.6783    -0.0700 0.020 0.384 0.208 0.372 0.004 0.012
#&gt; ERR519467     1  0.1180     0.7989 0.960 0.024 0.004 0.004 0.000 0.008
#&gt; ERR519489     5  0.3670     0.5708 0.004 0.088 0.052 0.004 0.828 0.024
#&gt; ERR519494     3  0.4910     0.6681 0.000 0.108 0.736 0.076 0.076 0.004
#&gt; ERR519474     6  0.3161     0.6848 0.028 0.008 0.000 0.016 0.096 0.852
#&gt; ERR519505     4  0.4015     0.5470 0.000 0.120 0.076 0.784 0.000 0.020
#&gt; ERR519517     3  0.1736     0.7181 0.000 0.032 0.936 0.008 0.020 0.004
#&gt; ERR519484     4  0.3597     0.6148 0.000 0.036 0.032 0.844 0.032 0.056
#&gt; ERR519498     4  0.4141     0.5424 0.000 0.092 0.168 0.740 0.000 0.000
#&gt; ERR519490     3  0.5555     0.6354 0.000 0.140 0.660 0.004 0.152 0.044
#&gt; ERR519507     6  0.6370     0.2197 0.008 0.024 0.000 0.168 0.312 0.488
#&gt; ERR519511     4  0.4848     0.3235 0.004 0.028 0.000 0.652 0.284 0.032
#&gt; ERR519468     3  0.2007     0.7086 0.000 0.040 0.924 0.012 0.016 0.008
#&gt; ERR519482     3  0.4665     0.6860 0.000 0.092 0.740 0.004 0.136 0.028
#&gt; ERR519475     2  0.8433     0.3684 0.140 0.452 0.036 0.108 0.084 0.180
#&gt; ERR519496     1  0.3473     0.6828 0.780 0.024 0.000 0.004 0.000 0.192
#&gt; ERR519506     6  0.1842     0.6857 0.012 0.012 0.000 0.036 0.008 0.932
#&gt; ERR519469     3  0.7872     0.1114 0.136 0.044 0.368 0.004 0.336 0.112
#&gt; ERR519480     3  0.3791     0.6827 0.000 0.128 0.800 0.044 0.000 0.028
#&gt; ERR519487     3  0.3054     0.6269 0.000 0.040 0.840 0.116 0.000 0.004
#&gt; ERR519483     6  0.2400     0.6735 0.068 0.012 0.008 0.004 0.008 0.900
#&gt; ERR519477     2  0.8456     0.2033 0.012 0.312 0.240 0.276 0.064 0.096
#&gt; ERR519499     3  0.1294     0.7163 0.004 0.024 0.956 0.008 0.008 0.000
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-5-a').click(function(){
  $('#tab-MAD-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-get-signatures'>
<ul>
<li><a href='#tab-MAD-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-1-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-1"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-2-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-2"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-3-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-3"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-4-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-4"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-5-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-NMF-signature_compare](figure_cola/MAD-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-NMF-collect-classes](figure_cola/MAD-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:hclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "hclust"]
# you can also extract it by
# res = res_list["ATC:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 18140 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-hclust-collect-plots](figure_cola/ATC-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-hclust-select-partition-number](figure_cola/ATC-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.1117 0.889   0.889
#> 3 3 0.669           0.838       0.921         3.8080 0.563   0.508
#> 4 4 0.569           0.687       0.808         0.1560 1.000   1.000
#> 5 5 0.800           0.825       0.908         0.1423 0.814   0.597
#> 6 6 0.779           0.764       0.885         0.0442 0.987   0.955
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-get-classes'>
<ul>
<li><a href='#tab-ATC-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-hclust-get-classes-1'>
<p><a id='tab-ATC-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette p1 p2
#&gt; ERR519515     1       0          1  1  0
#&gt; ERR519516     1       0          1  1  0
#&gt; ERR519520     1       0          1  1  0
#&gt; ERR519513     1       0          1  1  0
#&gt; ERR519481     1       0          1  1  0
#&gt; ERR519491     1       0          1  1  0
#&gt; ERR519473     1       0          1  1  0
#&gt; ERR519518     1       0          1  1  0
#&gt; ERR519512     1       0          1  1  0
#&gt; ERR519521     1       0          1  1  0
#&gt; ERR519488     1       0          1  1  0
#&gt; ERR519493     1       0          1  1  0
#&gt; ERR519514     1       0          1  1  0
#&gt; ERR519479     1       0          1  1  0
#&gt; ERR519509     1       0          1  1  0
#&gt; ERR519472     1       0          1  1  0
#&gt; ERR519510     1       0          1  1  0
#&gt; ERR519470     1       0          1  1  0
#&gt; ERR519495     1       0          1  1  0
#&gt; ERR519522     1       0          1  1  0
#&gt; ERR519523     1       0          1  1  0
#&gt; ERR519503     1       0          1  1  0
#&gt; ERR519471     1       0          1  1  0
#&gt; ERR519500     1       0          1  1  0
#&gt; ERR519485     1       0          1  1  0
#&gt; ERR519476     2       0          1  0  1
#&gt; ERR519502     1       0          1  1  0
#&gt; ERR519486     1       0          1  1  0
#&gt; ERR519478     1       0          1  1  0
#&gt; ERR519497     1       0          1  1  0
#&gt; ERR519467     1       0          1  1  0
#&gt; ERR519489     1       0          1  1  0
#&gt; ERR519494     1       0          1  1  0
#&gt; ERR519474     1       0          1  1  0
#&gt; ERR519505     1       0          1  1  0
#&gt; ERR519517     1       0          1  1  0
#&gt; ERR519484     1       0          1  1  0
#&gt; ERR519498     1       0          1  1  0
#&gt; ERR519490     1       0          1  1  0
#&gt; ERR519507     1       0          1  1  0
#&gt; ERR519511     1       0          1  1  0
#&gt; ERR519468     1       0          1  1  0
#&gt; ERR519482     1       0          1  1  0
#&gt; ERR519475     2       0          1  0  1
#&gt; ERR519496     1       0          1  1  0
#&gt; ERR519506     1       0          1  1  0
#&gt; ERR519469     1       0          1  1  0
#&gt; ERR519480     1       0          1  1  0
#&gt; ERR519487     1       0          1  1  0
#&gt; ERR519483     1       0          1  1  0
#&gt; ERR519477     2       0          1  0  1
#&gt; ERR519499     1       0          1  1  0
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-1-a').click(function(){
  $('#tab-ATC-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-2'>
<p><a id='tab-ATC-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3
#&gt; ERR519515     1  0.0747      0.947 0.984  0 0.016
#&gt; ERR519516     1  0.0000      0.946 1.000  0 0.000
#&gt; ERR519520     3  0.0000      0.838 0.000  0 1.000
#&gt; ERR519513     3  0.0000      0.838 0.000  0 1.000
#&gt; ERR519481     3  0.5591      0.694 0.304  0 0.696
#&gt; ERR519491     1  0.0747      0.947 0.984  0 0.016
#&gt; ERR519473     3  0.0237      0.838 0.004  0 0.996
#&gt; ERR519518     3  0.0000      0.838 0.000  0 1.000
#&gt; ERR519512     3  0.0000      0.838 0.000  0 1.000
#&gt; ERR519521     3  0.0000      0.838 0.000  0 1.000
#&gt; ERR519488     1  0.0000      0.946 1.000  0 0.000
#&gt; ERR519493     1  0.0747      0.947 0.984  0 0.016
#&gt; ERR519514     1  0.0747      0.947 0.984  0 0.016
#&gt; ERR519479     3  0.5706      0.673 0.320  0 0.680
#&gt; ERR519509     1  0.0000      0.946 1.000  0 0.000
#&gt; ERR519472     3  0.5016      0.741 0.240  0 0.760
#&gt; ERR519510     1  0.0747      0.947 0.984  0 0.016
#&gt; ERR519470     1  0.0000      0.946 1.000  0 0.000
#&gt; ERR519495     3  0.5591      0.694 0.304  0 0.696
#&gt; ERR519522     3  0.5591      0.694 0.304  0 0.696
#&gt; ERR519523     3  0.0000      0.838 0.000  0 1.000
#&gt; ERR519503     1  0.6126      0.139 0.600  0 0.400
#&gt; ERR519471     1  0.0000      0.946 1.000  0 0.000
#&gt; ERR519500     3  0.5591      0.694 0.304  0 0.696
#&gt; ERR519485     1  0.0000      0.946 1.000  0 0.000
#&gt; ERR519476     2  0.0000      1.000 0.000  1 0.000
#&gt; ERR519502     3  0.5591      0.694 0.304  0 0.696
#&gt; ERR519486     1  0.4235      0.737 0.824  0 0.176
#&gt; ERR519478     1  0.0747      0.947 0.984  0 0.016
#&gt; ERR519497     3  0.0237      0.838 0.004  0 0.996
#&gt; ERR519467     3  0.5591      0.694 0.304  0 0.696
#&gt; ERR519489     3  0.5591      0.694 0.304  0 0.696
#&gt; ERR519494     3  0.0000      0.838 0.000  0 1.000
#&gt; ERR519474     1  0.0000      0.946 1.000  0 0.000
#&gt; ERR519505     3  0.5882      0.624 0.348  0 0.652
#&gt; ERR519517     3  0.0000      0.838 0.000  0 1.000
#&gt; ERR519484     1  0.0747      0.947 0.984  0 0.016
#&gt; ERR519498     3  0.1289      0.829 0.032  0 0.968
#&gt; ERR519490     3  0.0000      0.838 0.000  0 1.000
#&gt; ERR519507     3  0.5706      0.673 0.320  0 0.680
#&gt; ERR519511     1  0.0747      0.947 0.984  0 0.016
#&gt; ERR519468     3  0.0000      0.838 0.000  0 1.000
#&gt; ERR519482     3  0.0000      0.838 0.000  0 1.000
#&gt; ERR519475     2  0.0000      1.000 0.000  1 0.000
#&gt; ERR519496     1  0.0747      0.947 0.984  0 0.016
#&gt; ERR519506     1  0.0000      0.946 1.000  0 0.000
#&gt; ERR519469     3  0.0237      0.838 0.004  0 0.996
#&gt; ERR519480     3  0.0000      0.838 0.000  0 1.000
#&gt; ERR519487     3  0.0000      0.838 0.000  0 1.000
#&gt; ERR519483     1  0.0000      0.946 1.000  0 0.000
#&gt; ERR519477     2  0.0000      1.000 0.000  1 0.000
#&gt; ERR519499     3  0.0000      0.838 0.000  0 1.000
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-2-a').click(function(){
  $('#tab-ATC-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-3'>
<p><a id='tab-ATC-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2 p3    p4
#&gt; ERR519515     1   0.000      0.896 1.000  0 NA 0.000
#&gt; ERR519516     1   0.194      0.883 0.924  0 NA 0.000
#&gt; ERR519520     4   0.000      0.661 0.000  0 NA 1.000
#&gt; ERR519513     4   0.147      0.661 0.000  0 NA 0.948
#&gt; ERR519481     4   0.758      0.474 0.308  0 NA 0.472
#&gt; ERR519491     1   0.000      0.896 1.000  0 NA 0.000
#&gt; ERR519473     4   0.209      0.663 0.020  0 NA 0.932
#&gt; ERR519518     4   0.000      0.661 0.000  0 NA 1.000
#&gt; ERR519512     4   0.000      0.661 0.000  0 NA 1.000
#&gt; ERR519521     4   0.000      0.661 0.000  0 NA 1.000
#&gt; ERR519488     1   0.194      0.883 0.924  0 NA 0.000
#&gt; ERR519493     1   0.000      0.896 1.000  0 NA 0.000
#&gt; ERR519514     1   0.000      0.896 1.000  0 NA 0.000
#&gt; ERR519479     4   0.762      0.453 0.324  0 NA 0.456
#&gt; ERR519509     1   0.194      0.883 0.924  0 NA 0.000
#&gt; ERR519472     4   0.579      0.584 0.244  0 NA 0.680
#&gt; ERR519510     1   0.000      0.896 1.000  0 NA 0.000
#&gt; ERR519470     1   0.194      0.883 0.924  0 NA 0.000
#&gt; ERR519495     4   0.758      0.474 0.308  0 NA 0.472
#&gt; ERR519522     4   0.758      0.474 0.308  0 NA 0.472
#&gt; ERR519523     4   0.000      0.661 0.000  0 NA 1.000
#&gt; ERR519503     1   0.687      0.163 0.580  0 NA 0.272
#&gt; ERR519471     1   0.194      0.883 0.924  0 NA 0.000
#&gt; ERR519500     4   0.758      0.474 0.308  0 NA 0.472
#&gt; ERR519485     1   0.194      0.883 0.924  0 NA 0.000
#&gt; ERR519476     2   0.000      1.000 0.000  1 NA 0.000
#&gt; ERR519502     4   0.758      0.474 0.308  0 NA 0.472
#&gt; ERR519486     1   0.473      0.697 0.780  0 NA 0.160
#&gt; ERR519478     1   0.000      0.896 1.000  0 NA 0.000
#&gt; ERR519497     4   0.217      0.662 0.020  0 NA 0.928
#&gt; ERR519467     4   0.758      0.474 0.308  0 NA 0.472
#&gt; ERR519489     4   0.758      0.474 0.308  0 NA 0.472
#&gt; ERR519494     4   0.365      0.579 0.000  0 NA 0.796
#&gt; ERR519474     1   0.194      0.883 0.924  0 NA 0.000
#&gt; ERR519505     4   0.774      0.413 0.328  0 NA 0.428
#&gt; ERR519517     4   0.369      0.577 0.000  0 NA 0.792
#&gt; ERR519484     1   0.000      0.896 1.000  0 NA 0.000
#&gt; ERR519498     4   0.282      0.658 0.036  0 NA 0.900
#&gt; ERR519490     4   0.369      0.577 0.000  0 NA 0.792
#&gt; ERR519507     4   0.762      0.453 0.324  0 NA 0.456
#&gt; ERR519511     1   0.000      0.896 1.000  0 NA 0.000
#&gt; ERR519468     4   0.369      0.577 0.000  0 NA 0.792
#&gt; ERR519482     4   0.369      0.577 0.000  0 NA 0.792
#&gt; ERR519475     2   0.000      1.000 0.000  1 NA 0.000
#&gt; ERR519496     1   0.000      0.896 1.000  0 NA 0.000
#&gt; ERR519506     1   0.297      0.818 0.856  0 NA 0.000
#&gt; ERR519469     4   0.209      0.663 0.020  0 NA 0.932
#&gt; ERR519480     4   0.369      0.577 0.000  0 NA 0.792
#&gt; ERR519487     4   0.369      0.577 0.000  0 NA 0.792
#&gt; ERR519483     1   0.497      0.369 0.544  0 NA 0.000
#&gt; ERR519477     2   0.000      1.000 0.000  1 NA 0.000
#&gt; ERR519499     4   0.369      0.577 0.000  0 NA 0.792
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-3-a').click(function(){
  $('#tab-ATC-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-4'>
<p><a id='tab-ATC-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3    p4    p5
#&gt; ERR519515     1  0.1671      0.924 0.924  0 0.000 0.076 0.000
#&gt; ERR519516     1  0.0000      0.908 1.000  0 0.000 0.000 0.000
#&gt; ERR519520     3  0.3305      0.811 0.000  0 0.776 0.224 0.000
#&gt; ERR519513     3  0.3661      0.775 0.000  0 0.724 0.276 0.000
#&gt; ERR519481     4  0.0162      0.918 0.000  0 0.004 0.996 0.000
#&gt; ERR519491     1  0.1671      0.924 0.924  0 0.000 0.076 0.000
#&gt; ERR519473     3  0.3857      0.736 0.000  0 0.688 0.312 0.000
#&gt; ERR519518     3  0.3305      0.811 0.000  0 0.776 0.224 0.000
#&gt; ERR519512     3  0.3305      0.811 0.000  0 0.776 0.224 0.000
#&gt; ERR519521     3  0.3305      0.811 0.000  0 0.776 0.224 0.000
#&gt; ERR519488     1  0.0000      0.908 1.000  0 0.000 0.000 0.000
#&gt; ERR519493     1  0.1671      0.924 0.924  0 0.000 0.076 0.000
#&gt; ERR519514     1  0.1671      0.924 0.924  0 0.000 0.076 0.000
#&gt; ERR519479     4  0.0404      0.908 0.012  0 0.000 0.988 0.000
#&gt; ERR519509     1  0.0000      0.908 1.000  0 0.000 0.000 0.000
#&gt; ERR519472     4  0.3210      0.620 0.000  0 0.212 0.788 0.000
#&gt; ERR519510     1  0.1671      0.924 0.924  0 0.000 0.076 0.000
#&gt; ERR519470     1  0.0000      0.908 1.000  0 0.000 0.000 0.000
#&gt; ERR519495     4  0.0162      0.918 0.000  0 0.004 0.996 0.000
#&gt; ERR519522     4  0.0162      0.918 0.000  0 0.004 0.996 0.000
#&gt; ERR519523     3  0.3305      0.811 0.000  0 0.776 0.224 0.000
#&gt; ERR519503     4  0.4768      0.344 0.304  0 0.000 0.656 0.040
#&gt; ERR519471     1  0.0000      0.908 1.000  0 0.000 0.000 0.000
#&gt; ERR519500     4  0.0162      0.918 0.000  0 0.004 0.996 0.000
#&gt; ERR519485     1  0.0000      0.908 1.000  0 0.000 0.000 0.000
#&gt; ERR519476     2  0.0000      1.000 0.000  1 0.000 0.000 0.000
#&gt; ERR519502     4  0.0162      0.918 0.000  0 0.004 0.996 0.000
#&gt; ERR519486     1  0.3300      0.673 0.792  0 0.004 0.204 0.000
#&gt; ERR519478     1  0.1671      0.924 0.924  0 0.000 0.076 0.000
#&gt; ERR519497     3  0.3857      0.738 0.000  0 0.688 0.312 0.000
#&gt; ERR519467     4  0.0162      0.918 0.000  0 0.004 0.996 0.000
#&gt; ERR519489     4  0.0162      0.918 0.000  0 0.004 0.996 0.000
#&gt; ERR519494     3  0.0162      0.786 0.000  0 0.996 0.004 0.000
#&gt; ERR519474     1  0.0000      0.908 1.000  0 0.000 0.000 0.000
#&gt; ERR519505     4  0.1300      0.886 0.016  0 0.000 0.956 0.028
#&gt; ERR519517     3  0.0000      0.785 0.000  0 1.000 0.000 0.000
#&gt; ERR519484     1  0.1671      0.924 0.924  0 0.000 0.076 0.000
#&gt; ERR519498     3  0.4300      0.405 0.000  0 0.524 0.476 0.000
#&gt; ERR519490     3  0.0000      0.785 0.000  0 1.000 0.000 0.000
#&gt; ERR519507     4  0.0404      0.908 0.012  0 0.000 0.988 0.000
#&gt; ERR519511     1  0.1671      0.924 0.924  0 0.000 0.076 0.000
#&gt; ERR519468     3  0.0000      0.785 0.000  0 1.000 0.000 0.000
#&gt; ERR519482     3  0.0000      0.785 0.000  0 1.000 0.000 0.000
#&gt; ERR519475     2  0.0000      1.000 0.000  1 0.000 0.000 0.000
#&gt; ERR519496     1  0.1671      0.924 0.924  0 0.000 0.076 0.000
#&gt; ERR519506     1  0.3143      0.744 0.796  0 0.000 0.000 0.204
#&gt; ERR519469     3  0.3857      0.736 0.000  0 0.688 0.312 0.000
#&gt; ERR519480     3  0.0162      0.783 0.000  0 0.996 0.000 0.004
#&gt; ERR519487     3  0.0000      0.785 0.000  0 1.000 0.000 0.000
#&gt; ERR519483     5  0.3177      0.000 0.208  0 0.000 0.000 0.792
#&gt; ERR519477     2  0.0000      1.000 0.000  1 0.000 0.000 0.000
#&gt; ERR519499     3  0.0000      0.785 0.000  0 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-4-a').click(function(){
  $('#tab-ATC-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-5'>
<p><a id='tab-ATC-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3    p4    p5    p6
#&gt; ERR519515     1  0.1141      0.907 0.948  0 0.000 0.000 0.052 0.000
#&gt; ERR519516     1  0.0632      0.884 0.976  0 0.000 0.024 0.000 0.000
#&gt; ERR519520     3  0.3315      0.758 0.000  0 0.780 0.000 0.200 0.020
#&gt; ERR519513     3  0.4120      0.692 0.000  0 0.728 0.000 0.068 0.204
#&gt; ERR519481     5  0.0000      0.884 0.000  0 0.000 0.000 1.000 0.000
#&gt; ERR519491     1  0.1141      0.907 0.948  0 0.000 0.000 0.052 0.000
#&gt; ERR519473     3  0.3879      0.685 0.000  0 0.688 0.000 0.292 0.020
#&gt; ERR519518     3  0.3315      0.758 0.000  0 0.780 0.000 0.200 0.020
#&gt; ERR519512     3  0.3315      0.758 0.000  0 0.780 0.000 0.200 0.020
#&gt; ERR519521     3  0.3315      0.758 0.000  0 0.780 0.000 0.200 0.020
#&gt; ERR519488     1  0.0632      0.884 0.976  0 0.000 0.024 0.000 0.000
#&gt; ERR519493     1  0.1141      0.907 0.948  0 0.000 0.000 0.052 0.000
#&gt; ERR519514     1  0.1141      0.907 0.948  0 0.000 0.000 0.052 0.000
#&gt; ERR519479     5  0.0865      0.864 0.036  0 0.000 0.000 0.964 0.000
#&gt; ERR519509     1  0.0632      0.884 0.976  0 0.000 0.024 0.000 0.000
#&gt; ERR519472     5  0.3403      0.611 0.000  0 0.212 0.000 0.768 0.020
#&gt; ERR519510     1  0.1141      0.907 0.948  0 0.000 0.000 0.052 0.000
#&gt; ERR519470     1  0.0632      0.884 0.976  0 0.000 0.024 0.000 0.000
#&gt; ERR519495     5  0.0000      0.884 0.000  0 0.000 0.000 1.000 0.000
#&gt; ERR519522     5  0.0000      0.884 0.000  0 0.000 0.000 1.000 0.000
#&gt; ERR519523     3  0.3315      0.758 0.000  0 0.780 0.000 0.200 0.020
#&gt; ERR519503     5  0.5438      0.211 0.284  0 0.000 0.016 0.592 0.108
#&gt; ERR519471     1  0.0632      0.884 0.976  0 0.000 0.024 0.000 0.000
#&gt; ERR519500     5  0.0000      0.884 0.000  0 0.000 0.000 1.000 0.000
#&gt; ERR519485     1  0.0632      0.884 0.976  0 0.000 0.024 0.000 0.000
#&gt; ERR519476     2  0.0000      1.000 0.000  1 0.000 0.000 0.000 0.000
#&gt; ERR519502     5  0.0000      0.884 0.000  0 0.000 0.000 1.000 0.000
#&gt; ERR519486     1  0.2838      0.457 0.808  0 0.004 0.000 0.188 0.000
#&gt; ERR519478     1  0.1141      0.907 0.948  0 0.000 0.000 0.052 0.000
#&gt; ERR519497     3  0.4587      0.671 0.000  0 0.688 0.000 0.108 0.204
#&gt; ERR519467     5  0.0000      0.884 0.000  0 0.000 0.000 1.000 0.000
#&gt; ERR519489     5  0.0000      0.884 0.000  0 0.000 0.000 1.000 0.000
#&gt; ERR519494     3  0.2340      0.692 0.000  0 0.852 0.148 0.000 0.000
#&gt; ERR519474     1  0.0632      0.884 0.976  0 0.000 0.024 0.000 0.000
#&gt; ERR519505     5  0.4527      0.573 0.024  0 0.000 0.044 0.704 0.228
#&gt; ERR519517     3  0.2482      0.690 0.000  0 0.848 0.148 0.000 0.004
#&gt; ERR519484     1  0.1141      0.907 0.948  0 0.000 0.000 0.052 0.000
#&gt; ERR519498     3  0.6000      0.443 0.016  0 0.528 0.000 0.252 0.204
#&gt; ERR519490     3  0.0146      0.748 0.000  0 0.996 0.000 0.000 0.004
#&gt; ERR519507     5  0.0865      0.864 0.036  0 0.000 0.000 0.964 0.000
#&gt; ERR519511     1  0.1141      0.907 0.948  0 0.000 0.000 0.052 0.000
#&gt; ERR519468     3  0.0146      0.748 0.000  0 0.996 0.000 0.000 0.004
#&gt; ERR519482     3  0.0146      0.748 0.000  0 0.996 0.000 0.000 0.004
#&gt; ERR519475     2  0.0000      1.000 0.000  1 0.000 0.000 0.000 0.000
#&gt; ERR519496     1  0.1141      0.907 0.948  0 0.000 0.000 0.052 0.000
#&gt; ERR519506     6  0.3765      0.000 0.404  0 0.000 0.000 0.000 0.596
#&gt; ERR519469     3  0.3879      0.685 0.000  0 0.688 0.000 0.292 0.020
#&gt; ERR519480     3  0.3432      0.653 0.000  0 0.800 0.148 0.000 0.052
#&gt; ERR519487     3  0.2482      0.690 0.000  0 0.848 0.148 0.000 0.004
#&gt; ERR519483     4  0.3307      0.000 0.044  0 0.000 0.808 0.000 0.148
#&gt; ERR519477     2  0.0000      1.000 0.000  1 0.000 0.000 0.000 0.000
#&gt; ERR519499     3  0.2482      0.690 0.000  0 0.848 0.148 0.000 0.004
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-5-a').click(function(){
  $('#tab-ATC-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-get-signatures'>
<ul>
<li><a href='#tab-ATC-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-1-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-1"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-2-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-2"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-3-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-3"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-4-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-4"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-5-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-hclust-signature_compare](figure_cola/ATC-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-hclust-collect-classes](figure_cola/ATC-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:kmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "kmeans"]
# you can also extract it by
# res = res_list["ATC:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 18140 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-kmeans-collect-plots](figure_cola/ATC-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-kmeans-select-partition-number](figure_cola/ATC-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.1117 0.889   0.889
#> 3 3 0.962           0.949       0.980         4.0272 0.549   0.493
#> 4 4 0.678           0.805       0.880         0.2222 0.824   0.618
#> 5 5 0.696           0.694       0.808         0.0798 0.959   0.869
#> 6 6 0.691           0.563       0.764         0.0548 0.961   0.856
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-get-classes'>
<ul>
<li><a href='#tab-ATC-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-kmeans-get-classes-1'>
<p><a id='tab-ATC-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette p1 p2
#&gt; ERR519515     1       0          1  1  0
#&gt; ERR519516     1       0          1  1  0
#&gt; ERR519520     1       0          1  1  0
#&gt; ERR519513     1       0          1  1  0
#&gt; ERR519481     1       0          1  1  0
#&gt; ERR519491     1       0          1  1  0
#&gt; ERR519473     1       0          1  1  0
#&gt; ERR519518     1       0          1  1  0
#&gt; ERR519512     1       0          1  1  0
#&gt; ERR519521     1       0          1  1  0
#&gt; ERR519488     1       0          1  1  0
#&gt; ERR519493     1       0          1  1  0
#&gt; ERR519514     1       0          1  1  0
#&gt; ERR519479     1       0          1  1  0
#&gt; ERR519509     1       0          1  1  0
#&gt; ERR519472     1       0          1  1  0
#&gt; ERR519510     1       0          1  1  0
#&gt; ERR519470     1       0          1  1  0
#&gt; ERR519495     1       0          1  1  0
#&gt; ERR519522     1       0          1  1  0
#&gt; ERR519523     1       0          1  1  0
#&gt; ERR519503     1       0          1  1  0
#&gt; ERR519471     1       0          1  1  0
#&gt; ERR519500     1       0          1  1  0
#&gt; ERR519485     1       0          1  1  0
#&gt; ERR519476     2       0          1  0  1
#&gt; ERR519502     1       0          1  1  0
#&gt; ERR519486     1       0          1  1  0
#&gt; ERR519478     1       0          1  1  0
#&gt; ERR519497     1       0          1  1  0
#&gt; ERR519467     1       0          1  1  0
#&gt; ERR519489     1       0          1  1  0
#&gt; ERR519494     1       0          1  1  0
#&gt; ERR519474     1       0          1  1  0
#&gt; ERR519505     1       0          1  1  0
#&gt; ERR519517     1       0          1  1  0
#&gt; ERR519484     1       0          1  1  0
#&gt; ERR519498     1       0          1  1  0
#&gt; ERR519490     1       0          1  1  0
#&gt; ERR519507     1       0          1  1  0
#&gt; ERR519511     1       0          1  1  0
#&gt; ERR519468     1       0          1  1  0
#&gt; ERR519482     1       0          1  1  0
#&gt; ERR519475     2       0          1  0  1
#&gt; ERR519496     1       0          1  1  0
#&gt; ERR519506     1       0          1  1  0
#&gt; ERR519469     1       0          1  1  0
#&gt; ERR519480     1       0          1  1  0
#&gt; ERR519487     1       0          1  1  0
#&gt; ERR519483     1       0          1  1  0
#&gt; ERR519477     2       0          1  0  1
#&gt; ERR519499     1       0          1  1  0
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-1-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-2'>
<p><a id='tab-ATC-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3
#&gt; ERR519515     1  0.0000      1.000 1.000  0 0.000
#&gt; ERR519516     1  0.0000      1.000 1.000  0 0.000
#&gt; ERR519520     3  0.0000      0.945 0.000  0 1.000
#&gt; ERR519513     3  0.0000      0.945 0.000  0 1.000
#&gt; ERR519481     3  0.0000      0.945 0.000  0 1.000
#&gt; ERR519491     1  0.0000      1.000 1.000  0 0.000
#&gt; ERR519473     3  0.0000      0.945 0.000  0 1.000
#&gt; ERR519518     3  0.0000      0.945 0.000  0 1.000
#&gt; ERR519512     3  0.0000      0.945 0.000  0 1.000
#&gt; ERR519521     3  0.0000      0.945 0.000  0 1.000
#&gt; ERR519488     1  0.0000      1.000 1.000  0 0.000
#&gt; ERR519493     1  0.0000      1.000 1.000  0 0.000
#&gt; ERR519514     1  0.0000      1.000 1.000  0 0.000
#&gt; ERR519479     1  0.0000      1.000 1.000  0 0.000
#&gt; ERR519509     1  0.0000      1.000 1.000  0 0.000
#&gt; ERR519472     3  0.0237      0.942 0.004  0 0.996
#&gt; ERR519510     1  0.0000      1.000 1.000  0 0.000
#&gt; ERR519470     1  0.0000      1.000 1.000  0 0.000
#&gt; ERR519495     3  0.4399      0.745 0.188  0 0.812
#&gt; ERR519522     3  0.4555      0.729 0.200  0 0.800
#&gt; ERR519523     3  0.0000      0.945 0.000  0 1.000
#&gt; ERR519503     1  0.0000      1.000 1.000  0 0.000
#&gt; ERR519471     1  0.0000      1.000 1.000  0 0.000
#&gt; ERR519500     3  0.6095      0.410 0.392  0 0.608
#&gt; ERR519485     1  0.0000      1.000 1.000  0 0.000
#&gt; ERR519476     2  0.0000      1.000 0.000  1 0.000
#&gt; ERR519502     3  0.0000      0.945 0.000  0 1.000
#&gt; ERR519486     1  0.0000      1.000 1.000  0 0.000
#&gt; ERR519478     1  0.0000      1.000 1.000  0 0.000
#&gt; ERR519497     3  0.0000      0.945 0.000  0 1.000
#&gt; ERR519467     3  0.4605      0.724 0.204  0 0.796
#&gt; ERR519489     3  0.0000      0.945 0.000  0 1.000
#&gt; ERR519494     3  0.0000      0.945 0.000  0 1.000
#&gt; ERR519474     1  0.0000      1.000 1.000  0 0.000
#&gt; ERR519505     1  0.0000      1.000 1.000  0 0.000
#&gt; ERR519517     3  0.0000      0.945 0.000  0 1.000
#&gt; ERR519484     1  0.0000      1.000 1.000  0 0.000
#&gt; ERR519498     3  0.1860      0.897 0.052  0 0.948
#&gt; ERR519490     3  0.0000      0.945 0.000  0 1.000
#&gt; ERR519507     1  0.0000      1.000 1.000  0 0.000
#&gt; ERR519511     1  0.0000      1.000 1.000  0 0.000
#&gt; ERR519468     3  0.0000      0.945 0.000  0 1.000
#&gt; ERR519482     3  0.0000      0.945 0.000  0 1.000
#&gt; ERR519475     2  0.0000      1.000 0.000  1 0.000
#&gt; ERR519496     1  0.0000      1.000 1.000  0 0.000
#&gt; ERR519506     1  0.0000      1.000 1.000  0 0.000
#&gt; ERR519469     3  0.0000      0.945 0.000  0 1.000
#&gt; ERR519480     3  0.0000      0.945 0.000  0 1.000
#&gt; ERR519487     3  0.0000      0.945 0.000  0 1.000
#&gt; ERR519483     1  0.0000      1.000 1.000  0 0.000
#&gt; ERR519477     2  0.0000      1.000 0.000  1 0.000
#&gt; ERR519499     3  0.0000      0.945 0.000  0 1.000
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-2-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-3'>
<p><a id='tab-ATC-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3    p4
#&gt; ERR519515     1   0.000      0.875 1.000  0 0.000 0.000
#&gt; ERR519516     1   0.000      0.875 1.000  0 0.000 0.000
#&gt; ERR519520     4   0.483      0.494 0.000  0 0.392 0.608
#&gt; ERR519513     3   0.344      0.805 0.000  0 0.816 0.184
#&gt; ERR519481     4   0.112      0.785 0.000  0 0.036 0.964
#&gt; ERR519491     1   0.234      0.877 0.900  0 0.000 0.100
#&gt; ERR519473     4   0.483      0.494 0.000  0 0.392 0.608
#&gt; ERR519518     3   0.344      0.804 0.000  0 0.816 0.184
#&gt; ERR519512     4   0.483      0.494 0.000  0 0.392 0.608
#&gt; ERR519521     4   0.483      0.494 0.000  0 0.392 0.608
#&gt; ERR519488     1   0.000      0.875 1.000  0 0.000 0.000
#&gt; ERR519493     1   0.234      0.877 0.900  0 0.000 0.100
#&gt; ERR519514     1   0.281      0.868 0.868  0 0.000 0.132
#&gt; ERR519479     4   0.215      0.718 0.088  0 0.000 0.912
#&gt; ERR519509     1   0.000      0.875 1.000  0 0.000 0.000
#&gt; ERR519472     4   0.112      0.785 0.000  0 0.036 0.964
#&gt; ERR519510     1   0.281      0.868 0.868  0 0.000 0.132
#&gt; ERR519470     1   0.000      0.875 1.000  0 0.000 0.000
#&gt; ERR519495     4   0.121      0.777 0.032  0 0.004 0.964
#&gt; ERR519522     4   0.112      0.775 0.036  0 0.000 0.964
#&gt; ERR519523     4   0.483      0.494 0.000  0 0.392 0.608
#&gt; ERR519503     1   0.604      0.563 0.560  0 0.048 0.392
#&gt; ERR519471     1   0.000      0.875 1.000  0 0.000 0.000
#&gt; ERR519500     4   0.140      0.772 0.040  0 0.004 0.956
#&gt; ERR519485     1   0.000      0.875 1.000  0 0.000 0.000
#&gt; ERR519476     2   0.000      1.000 0.000  1 0.000 0.000
#&gt; ERR519502     4   0.112      0.785 0.000  0 0.036 0.964
#&gt; ERR519486     1   0.384      0.789 0.776  0 0.000 0.224
#&gt; ERR519478     1   0.247      0.875 0.892  0 0.000 0.108
#&gt; ERR519497     4   0.441      0.610 0.000  0 0.300 0.700
#&gt; ERR519467     4   0.112      0.775 0.036  0 0.000 0.964
#&gt; ERR519489     4   0.112      0.785 0.000  0 0.036 0.964
#&gt; ERR519494     3   0.147      0.958 0.000  0 0.948 0.052
#&gt; ERR519474     1   0.000      0.875 1.000  0 0.000 0.000
#&gt; ERR519505     1   0.620      0.476 0.508  0 0.052 0.440
#&gt; ERR519517     3   0.147      0.958 0.000  0 0.948 0.052
#&gt; ERR519484     1   0.281      0.868 0.868  0 0.000 0.132
#&gt; ERR519498     4   0.121      0.784 0.004  0 0.032 0.964
#&gt; ERR519490     3   0.147      0.958 0.000  0 0.948 0.052
#&gt; ERR519507     4   0.215      0.718 0.088  0 0.000 0.912
#&gt; ERR519511     1   0.292      0.864 0.860  0 0.000 0.140
#&gt; ERR519468     3   0.147      0.958 0.000  0 0.948 0.052
#&gt; ERR519482     3   0.147      0.958 0.000  0 0.948 0.052
#&gt; ERR519475     2   0.000      1.000 0.000  1 0.000 0.000
#&gt; ERR519496     1   0.292      0.864 0.860  0 0.000 0.140
#&gt; ERR519506     1   0.240      0.828 0.920  0 0.048 0.032
#&gt; ERR519469     4   0.448      0.598 0.000  0 0.312 0.688
#&gt; ERR519480     3   0.147      0.958 0.000  0 0.948 0.052
#&gt; ERR519487     3   0.147      0.958 0.000  0 0.948 0.052
#&gt; ERR519483     1   0.161      0.849 0.952  0 0.016 0.032
#&gt; ERR519477     2   0.000      1.000 0.000  1 0.000 0.000
#&gt; ERR519499     3   0.147      0.958 0.000  0 0.948 0.052
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-3-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-4'>
<p><a id='tab-ATC-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3    p4    p5
#&gt; ERR519515     1  0.0609      0.795 0.980  0 0.000 0.000 0.020
#&gt; ERR519516     1  0.0162      0.790 0.996  0 0.000 0.000 0.004
#&gt; ERR519520     4  0.6448      0.484 0.000  0 0.272 0.500 0.228
#&gt; ERR519513     3  0.5891      0.458 0.000  0 0.552 0.120 0.328
#&gt; ERR519481     4  0.1168      0.674 0.000  0 0.008 0.960 0.032
#&gt; ERR519491     1  0.3692      0.781 0.812  0 0.000 0.052 0.136
#&gt; ERR519473     4  0.6448      0.482 0.000  0 0.272 0.500 0.228
#&gt; ERR519518     3  0.5950      0.408 0.000  0 0.592 0.188 0.220
#&gt; ERR519512     4  0.6448      0.484 0.000  0 0.272 0.500 0.228
#&gt; ERR519521     4  0.6428      0.487 0.000  0 0.272 0.504 0.224
#&gt; ERR519488     1  0.0510      0.784 0.984  0 0.000 0.000 0.016
#&gt; ERR519493     1  0.3692      0.781 0.812  0 0.000 0.052 0.136
#&gt; ERR519514     1  0.4069      0.767 0.788  0 0.000 0.076 0.136
#&gt; ERR519479     4  0.2915      0.497 0.024  0 0.000 0.860 0.116
#&gt; ERR519509     1  0.0510      0.784 0.984  0 0.000 0.000 0.016
#&gt; ERR519472     4  0.0290      0.667 0.000  0 0.008 0.992 0.000
#&gt; ERR519510     1  0.4334      0.749 0.764  0 0.000 0.080 0.156
#&gt; ERR519470     1  0.0000      0.791 1.000  0 0.000 0.000 0.000
#&gt; ERR519495     4  0.0693      0.656 0.008  0 0.000 0.980 0.012
#&gt; ERR519522     4  0.1331      0.667 0.008  0 0.000 0.952 0.040
#&gt; ERR519523     4  0.6428      0.487 0.000  0 0.272 0.504 0.224
#&gt; ERR519503     5  0.6465      0.653 0.208  0 0.000 0.308 0.484
#&gt; ERR519471     1  0.0880      0.795 0.968  0 0.000 0.000 0.032
#&gt; ERR519500     4  0.0898      0.649 0.008  0 0.000 0.972 0.020
#&gt; ERR519485     1  0.0609      0.783 0.980  0 0.000 0.000 0.020
#&gt; ERR519476     2  0.0000      1.000 0.000  1 0.000 0.000 0.000
#&gt; ERR519502     4  0.1408      0.674 0.000  0 0.008 0.948 0.044
#&gt; ERR519486     1  0.5590      0.484 0.640  0 0.000 0.204 0.156
#&gt; ERR519478     1  0.3825      0.777 0.804  0 0.000 0.060 0.136
#&gt; ERR519497     4  0.6053      0.564 0.000  0 0.196 0.576 0.228
#&gt; ERR519467     4  0.0693      0.656 0.008  0 0.000 0.980 0.012
#&gt; ERR519489     4  0.0290      0.667 0.000  0 0.008 0.992 0.000
#&gt; ERR519494     3  0.1082      0.870 0.000  0 0.964 0.008 0.028
#&gt; ERR519474     1  0.0510      0.785 0.984  0 0.000 0.000 0.016
#&gt; ERR519505     5  0.5461      0.570 0.096  0 0.000 0.284 0.620
#&gt; ERR519517     3  0.0451      0.873 0.000  0 0.988 0.008 0.004
#&gt; ERR519484     1  0.4334      0.749 0.764  0 0.000 0.080 0.156
#&gt; ERR519498     4  0.4564      0.480 0.004  0 0.008 0.600 0.388
#&gt; ERR519490     3  0.0992      0.870 0.000  0 0.968 0.008 0.024
#&gt; ERR519507     4  0.2915      0.497 0.024  0 0.000 0.860 0.116
#&gt; ERR519511     1  0.4548      0.731 0.748  0 0.000 0.096 0.156
#&gt; ERR519468     3  0.0693      0.873 0.000  0 0.980 0.008 0.012
#&gt; ERR519482     3  0.0579      0.874 0.000  0 0.984 0.008 0.008
#&gt; ERR519475     2  0.0000      1.000 0.000  1 0.000 0.000 0.000
#&gt; ERR519496     1  0.4322      0.751 0.768  0 0.000 0.088 0.144
#&gt; ERR519506     5  0.4907      0.132 0.488  0 0.000 0.024 0.488
#&gt; ERR519469     4  0.6120      0.556 0.000  0 0.196 0.564 0.240
#&gt; ERR519480     3  0.2464      0.809 0.000  0 0.888 0.016 0.096
#&gt; ERR519487     3  0.0451      0.873 0.000  0 0.988 0.008 0.004
#&gt; ERR519483     1  0.1830      0.723 0.924  0 0.008 0.000 0.068
#&gt; ERR519477     2  0.0000      1.000 0.000  1 0.000 0.000 0.000
#&gt; ERR519499     3  0.0798      0.871 0.000  0 0.976 0.008 0.016
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-4-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-5'>
<p><a id='tab-ATC-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3    p4    p5    p6
#&gt; ERR519515     1  0.3352     0.7473 0.816  0 0.000 0.112 0.000 0.072
#&gt; ERR519516     1  0.4267     0.7235 0.732  0 0.000 0.152 0.000 0.116
#&gt; ERR519520     5  0.5392    -0.3945 0.000  0 0.112 0.440 0.448 0.000
#&gt; ERR519513     4  0.5771     0.2100 0.000  0 0.356 0.524 0.036 0.084
#&gt; ERR519481     5  0.0458     0.5965 0.000  0 0.000 0.016 0.984 0.000
#&gt; ERR519491     1  0.0603     0.7440 0.980  0 0.000 0.000 0.016 0.004
#&gt; ERR519473     4  0.5534     0.2949 0.000  0 0.132 0.444 0.424 0.000
#&gt; ERR519518     4  0.5400     0.3951 0.000  0 0.400 0.484 0.116 0.000
#&gt; ERR519512     5  0.5392    -0.3945 0.000  0 0.112 0.440 0.448 0.000
#&gt; ERR519521     5  0.5392    -0.3945 0.000  0 0.112 0.440 0.448 0.000
#&gt; ERR519488     1  0.4533     0.7091 0.704  0 0.000 0.156 0.000 0.140
#&gt; ERR519493     1  0.0603     0.7440 0.980  0 0.000 0.000 0.016 0.004
#&gt; ERR519514     1  0.0972     0.7377 0.964  0 0.000 0.000 0.028 0.008
#&gt; ERR519479     5  0.3906     0.3497 0.216  0 0.000 0.008 0.744 0.032
#&gt; ERR519509     1  0.4533     0.7091 0.704  0 0.000 0.156 0.000 0.140
#&gt; ERR519472     5  0.0000     0.6018 0.000  0 0.000 0.000 1.000 0.000
#&gt; ERR519510     1  0.2002     0.7109 0.916  0 0.000 0.008 0.020 0.056
#&gt; ERR519470     1  0.3953     0.7355 0.764  0 0.000 0.132 0.000 0.104
#&gt; ERR519495     5  0.0458     0.6006 0.016  0 0.000 0.000 0.984 0.000
#&gt; ERR519522     5  0.1151     0.5959 0.012  0 0.000 0.032 0.956 0.000
#&gt; ERR519523     5  0.5392    -0.3945 0.000  0 0.112 0.440 0.448 0.000
#&gt; ERR519503     6  0.5254     0.7286 0.220  0 0.000 0.004 0.156 0.620
#&gt; ERR519471     1  0.3361     0.7436 0.816  0 0.000 0.108 0.000 0.076
#&gt; ERR519500     5  0.1219     0.5824 0.048  0 0.000 0.000 0.948 0.004
#&gt; ERR519485     1  0.4603     0.7070 0.696  0 0.000 0.156 0.000 0.148
#&gt; ERR519476     2  0.0000     1.0000 0.000  1 0.000 0.000 0.000 0.000
#&gt; ERR519502     5  0.0458     0.5965 0.000  0 0.000 0.016 0.984 0.000
#&gt; ERR519486     1  0.3474     0.5767 0.820  0 0.000 0.012 0.112 0.056
#&gt; ERR519478     1  0.0632     0.7425 0.976  0 0.000 0.000 0.024 0.000
#&gt; ERR519497     5  0.5115    -0.3545 0.000  0 0.080 0.456 0.464 0.000
#&gt; ERR519467     5  0.0717     0.5988 0.016  0 0.000 0.008 0.976 0.000
#&gt; ERR519489     5  0.0000     0.6018 0.000  0 0.000 0.000 1.000 0.000
#&gt; ERR519494     3  0.1812     0.8825 0.000  0 0.912 0.080 0.000 0.008
#&gt; ERR519474     1  0.4603     0.7070 0.696  0 0.000 0.156 0.000 0.148
#&gt; ERR519505     6  0.6090     0.6436 0.144  0 0.000 0.136 0.108 0.612
#&gt; ERR519517     3  0.0632     0.9008 0.000  0 0.976 0.000 0.000 0.024
#&gt; ERR519484     1  0.2002     0.7109 0.916  0 0.000 0.008 0.020 0.056
#&gt; ERR519498     5  0.6066    -0.0367 0.032  0 0.000 0.420 0.432 0.116
#&gt; ERR519490     3  0.2357     0.8627 0.000  0 0.872 0.116 0.000 0.012
#&gt; ERR519507     5  0.3878     0.3553 0.212  0 0.000 0.008 0.748 0.032
#&gt; ERR519511     1  0.2563     0.6745 0.884  0 0.000 0.008 0.068 0.040
#&gt; ERR519468     3  0.1967     0.8847 0.000  0 0.904 0.084 0.000 0.012
#&gt; ERR519482     3  0.1913     0.8864 0.000  0 0.908 0.080 0.000 0.012
#&gt; ERR519475     2  0.0000     1.0000 0.000  1 0.000 0.000 0.000 0.000
#&gt; ERR519496     1  0.1794     0.7126 0.924  0 0.000 0.000 0.036 0.040
#&gt; ERR519506     6  0.3915     0.6394 0.288  0 0.000 0.016 0.004 0.692
#&gt; ERR519469     4  0.5350     0.3140 0.000  0 0.108 0.476 0.416 0.000
#&gt; ERR519480     3  0.3384     0.7943 0.000  0 0.812 0.068 0.000 0.120
#&gt; ERR519487     3  0.0632     0.9008 0.000  0 0.976 0.000 0.000 0.024
#&gt; ERR519483     1  0.5844     0.4169 0.488  0 0.000 0.244 0.000 0.268
#&gt; ERR519477     2  0.0000     1.0000 0.000  1 0.000 0.000 0.000 0.000
#&gt; ERR519499     3  0.1151     0.8948 0.000  0 0.956 0.012 0.000 0.032
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-5-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-get-signatures'>
<ul>
<li><a href='#tab-ATC-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-kmeans-signature_compare](figure_cola/ATC-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-kmeans-collect-classes](figure_cola/ATC-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:skmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "skmeans"]
# you can also extract it by
# res = res_list["ATC:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 18140 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-skmeans-collect-plots](figure_cola/ATC-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-skmeans-select-partition-number](figure_cola/ATC-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.992       0.996         0.4975 0.502   0.502
#> 3 3 0.728           0.487       0.780         0.3102 0.922   0.844
#> 4 4 0.647           0.557       0.722         0.0984 0.744   0.445
#> 5 5 0.679           0.664       0.827         0.0668 0.903   0.652
#> 6 6 0.695           0.546       0.761         0.0402 0.965   0.842
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-get-classes'>
<ul>
<li><a href='#tab-ATC-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-skmeans-get-classes-1'>
<p><a id='tab-ATC-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; ERR519515     2   0.000      0.993 0.000 1.000
#&gt; ERR519516     2   0.000      0.993 0.000 1.000
#&gt; ERR519520     1   0.000      0.999 1.000 0.000
#&gt; ERR519513     1   0.000      0.999 1.000 0.000
#&gt; ERR519481     1   0.000      0.999 1.000 0.000
#&gt; ERR519491     2   0.000      0.993 0.000 1.000
#&gt; ERR519473     1   0.000      0.999 1.000 0.000
#&gt; ERR519518     1   0.000      0.999 1.000 0.000
#&gt; ERR519512     1   0.000      0.999 1.000 0.000
#&gt; ERR519521     1   0.000      0.999 1.000 0.000
#&gt; ERR519488     2   0.000      0.993 0.000 1.000
#&gt; ERR519493     2   0.000      0.993 0.000 1.000
#&gt; ERR519514     2   0.000      0.993 0.000 1.000
#&gt; ERR519479     1   0.000      0.999 1.000 0.000
#&gt; ERR519509     2   0.000      0.993 0.000 1.000
#&gt; ERR519472     1   0.000      0.999 1.000 0.000
#&gt; ERR519510     2   0.000      0.993 0.000 1.000
#&gt; ERR519470     2   0.000      0.993 0.000 1.000
#&gt; ERR519495     1   0.000      0.999 1.000 0.000
#&gt; ERR519522     1   0.000      0.999 1.000 0.000
#&gt; ERR519523     1   0.000      0.999 1.000 0.000
#&gt; ERR519503     1   0.242      0.958 0.960 0.040
#&gt; ERR519471     2   0.000      0.993 0.000 1.000
#&gt; ERR519500     1   0.000      0.999 1.000 0.000
#&gt; ERR519485     2   0.000      0.993 0.000 1.000
#&gt; ERR519476     2   0.000      0.993 0.000 1.000
#&gt; ERR519502     1   0.000      0.999 1.000 0.000
#&gt; ERR519486     2   0.625      0.816 0.156 0.844
#&gt; ERR519478     2   0.000      0.993 0.000 1.000
#&gt; ERR519497     1   0.000      0.999 1.000 0.000
#&gt; ERR519467     1   0.000      0.999 1.000 0.000
#&gt; ERR519489     1   0.000      0.999 1.000 0.000
#&gt; ERR519494     1   0.000      0.999 1.000 0.000
#&gt; ERR519474     2   0.000      0.993 0.000 1.000
#&gt; ERR519505     1   0.000      0.999 1.000 0.000
#&gt; ERR519517     1   0.000      0.999 1.000 0.000
#&gt; ERR519484     2   0.000      0.993 0.000 1.000
#&gt; ERR519498     1   0.000      0.999 1.000 0.000
#&gt; ERR519490     1   0.000      0.999 1.000 0.000
#&gt; ERR519507     1   0.000      0.999 1.000 0.000
#&gt; ERR519511     2   0.000      0.993 0.000 1.000
#&gt; ERR519468     1   0.000      0.999 1.000 0.000
#&gt; ERR519482     1   0.000      0.999 1.000 0.000
#&gt; ERR519475     2   0.000      0.993 0.000 1.000
#&gt; ERR519496     2   0.000      0.993 0.000 1.000
#&gt; ERR519506     2   0.000      0.993 0.000 1.000
#&gt; ERR519469     1   0.000      0.999 1.000 0.000
#&gt; ERR519480     1   0.000      0.999 1.000 0.000
#&gt; ERR519487     1   0.000      0.999 1.000 0.000
#&gt; ERR519483     2   0.000      0.993 0.000 1.000
#&gt; ERR519477     2   0.000      0.993 0.000 1.000
#&gt; ERR519499     1   0.000      0.999 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-1-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-2'>
<p><a id='tab-ATC-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; ERR519515     1  0.0000    0.96588 1.000 0.000 0.000
#&gt; ERR519516     1  0.0000    0.96588 1.000 0.000 0.000
#&gt; ERR519520     3  0.0000    0.24780 0.000 0.000 1.000
#&gt; ERR519513     3  0.6215    0.25475 0.000 0.428 0.572
#&gt; ERR519481     3  0.6079    0.07595 0.000 0.388 0.612
#&gt; ERR519491     1  0.1163    0.95409 0.972 0.028 0.000
#&gt; ERR519473     3  0.4452    0.19895 0.000 0.192 0.808
#&gt; ERR519518     3  0.2066    0.24598 0.000 0.060 0.940
#&gt; ERR519512     3  0.0000    0.24780 0.000 0.000 1.000
#&gt; ERR519521     3  0.4555    0.19531 0.000 0.200 0.800
#&gt; ERR519488     1  0.0000    0.96588 1.000 0.000 0.000
#&gt; ERR519493     1  0.1289    0.95204 0.968 0.032 0.000
#&gt; ERR519514     1  0.0000    0.96588 1.000 0.000 0.000
#&gt; ERR519479     2  0.6244    0.00527 0.000 0.560 0.440
#&gt; ERR519509     1  0.0000    0.96588 1.000 0.000 0.000
#&gt; ERR519472     3  0.6079    0.07595 0.000 0.388 0.612
#&gt; ERR519510     1  0.3879    0.86994 0.848 0.152 0.000
#&gt; ERR519470     1  0.0000    0.96588 1.000 0.000 0.000
#&gt; ERR519495     3  0.6079    0.07595 0.000 0.388 0.612
#&gt; ERR519522     3  0.5905    0.09853 0.000 0.352 0.648
#&gt; ERR519523     3  0.4504    0.19747 0.000 0.196 0.804
#&gt; ERR519503     2  0.8837   -0.21643 0.116 0.460 0.424
#&gt; ERR519471     1  0.0000    0.96588 1.000 0.000 0.000
#&gt; ERR519500     3  0.6140    0.04761 0.000 0.404 0.596
#&gt; ERR519485     1  0.0000    0.96588 1.000 0.000 0.000
#&gt; ERR519476     1  0.0000    0.96588 1.000 0.000 0.000
#&gt; ERR519502     3  0.6079    0.07595 0.000 0.388 0.612
#&gt; ERR519486     1  0.6351    0.77894 0.760 0.168 0.072
#&gt; ERR519478     1  0.0237    0.96471 0.996 0.004 0.000
#&gt; ERR519497     3  0.6180    0.25212 0.000 0.416 0.584
#&gt; ERR519467     3  0.6062    0.07942 0.000 0.384 0.616
#&gt; ERR519489     3  0.6062    0.07942 0.000 0.384 0.616
#&gt; ERR519494     3  0.6215    0.25475 0.000 0.428 0.572
#&gt; ERR519474     1  0.0000    0.96588 1.000 0.000 0.000
#&gt; ERR519505     2  0.6111   -0.19072 0.000 0.604 0.396
#&gt; ERR519517     3  0.6215    0.25475 0.000 0.428 0.572
#&gt; ERR519484     1  0.3879    0.86994 0.848 0.152 0.000
#&gt; ERR519498     3  0.6215    0.25475 0.000 0.428 0.572
#&gt; ERR519490     3  0.6215    0.25475 0.000 0.428 0.572
#&gt; ERR519507     2  0.6244    0.00527 0.000 0.560 0.440
#&gt; ERR519511     1  0.3879    0.86994 0.848 0.152 0.000
#&gt; ERR519468     3  0.6215    0.25475 0.000 0.428 0.572
#&gt; ERR519482     3  0.6215    0.25475 0.000 0.428 0.572
#&gt; ERR519475     1  0.0000    0.96588 1.000 0.000 0.000
#&gt; ERR519496     1  0.0237    0.96471 0.996 0.004 0.000
#&gt; ERR519506     1  0.1289    0.94838 0.968 0.032 0.000
#&gt; ERR519469     3  0.6204    0.25428 0.000 0.424 0.576
#&gt; ERR519480     3  0.6215    0.25475 0.000 0.428 0.572
#&gt; ERR519487     3  0.6215    0.25475 0.000 0.428 0.572
#&gt; ERR519483     1  0.0000    0.96588 1.000 0.000 0.000
#&gt; ERR519477     1  0.0000    0.96588 1.000 0.000 0.000
#&gt; ERR519499     3  0.6215    0.25475 0.000 0.428 0.572
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-2-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-3'>
<p><a id='tab-ATC-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; ERR519515     1  0.4994    -0.3852 0.520 0.480 0.000 0.000
#&gt; ERR519516     2  0.4877     0.6514 0.408 0.592 0.000 0.000
#&gt; ERR519520     3  0.5137    -0.0436 0.000 0.004 0.544 0.452
#&gt; ERR519513     3  0.0376     0.8168 0.004 0.004 0.992 0.000
#&gt; ERR519481     4  0.2011     0.7966 0.000 0.000 0.080 0.920
#&gt; ERR519491     1  0.3074     0.6034 0.848 0.152 0.000 0.000
#&gt; ERR519473     4  0.5132     0.3050 0.000 0.004 0.448 0.548
#&gt; ERR519518     3  0.4677     0.4012 0.000 0.004 0.680 0.316
#&gt; ERR519512     3  0.5137    -0.0436 0.000 0.004 0.544 0.452
#&gt; ERR519521     4  0.5080     0.3850 0.000 0.004 0.420 0.576
#&gt; ERR519488     2  0.4866     0.6568 0.404 0.596 0.000 0.000
#&gt; ERR519493     1  0.3266     0.5958 0.832 0.168 0.000 0.000
#&gt; ERR519514     1  0.4994    -0.3852 0.520 0.480 0.000 0.000
#&gt; ERR519479     4  0.4164     0.5942 0.264 0.000 0.000 0.736
#&gt; ERR519509     2  0.4877     0.6514 0.408 0.592 0.000 0.000
#&gt; ERR519472     4  0.2011     0.7966 0.000 0.000 0.080 0.920
#&gt; ERR519510     1  0.0336     0.5993 0.992 0.000 0.000 0.008
#&gt; ERR519470     2  0.4999     0.3872 0.492 0.508 0.000 0.000
#&gt; ERR519495     4  0.2011     0.7966 0.000 0.000 0.080 0.920
#&gt; ERR519522     4  0.3751     0.7326 0.000 0.004 0.196 0.800
#&gt; ERR519523     4  0.5088     0.3752 0.000 0.004 0.424 0.572
#&gt; ERR519503     3  0.6599     0.3140 0.000 0.432 0.488 0.080
#&gt; ERR519471     2  0.4855     0.6543 0.400 0.600 0.000 0.000
#&gt; ERR519500     4  0.2011     0.7966 0.000 0.000 0.080 0.920
#&gt; ERR519485     2  0.4898     0.6439 0.416 0.584 0.000 0.000
#&gt; ERR519476     2  0.4866     0.6568 0.404 0.596 0.000 0.000
#&gt; ERR519502     4  0.2593     0.7943 0.000 0.004 0.104 0.892
#&gt; ERR519486     1  0.6208     0.3547 0.672 0.216 0.108 0.004
#&gt; ERR519478     1  0.3975     0.5116 0.760 0.240 0.000 0.000
#&gt; ERR519497     3  0.3306     0.6903 0.000 0.004 0.840 0.156
#&gt; ERR519467     4  0.2408     0.7948 0.000 0.000 0.104 0.896
#&gt; ERR519489     4  0.3074     0.7715 0.000 0.000 0.152 0.848
#&gt; ERR519494     3  0.0592     0.8121 0.000 0.000 0.984 0.016
#&gt; ERR519474     2  0.4888     0.6501 0.412 0.588 0.000 0.000
#&gt; ERR519505     2  0.8498    -0.3848 0.116 0.408 0.400 0.076
#&gt; ERR519517     3  0.0000     0.8188 0.000 0.000 1.000 0.000
#&gt; ERR519484     1  0.0524     0.5995 0.988 0.004 0.000 0.008
#&gt; ERR519498     3  0.0657     0.8137 0.012 0.004 0.984 0.000
#&gt; ERR519490     3  0.0000     0.8188 0.000 0.000 1.000 0.000
#&gt; ERR519507     4  0.3907     0.6324 0.232 0.000 0.000 0.768
#&gt; ERR519511     1  0.0779     0.5962 0.980 0.004 0.000 0.016
#&gt; ERR519468     3  0.0000     0.8188 0.000 0.000 1.000 0.000
#&gt; ERR519482     3  0.0000     0.8188 0.000 0.000 1.000 0.000
#&gt; ERR519475     2  0.4866     0.6568 0.404 0.596 0.000 0.000
#&gt; ERR519496     1  0.3873     0.5258 0.772 0.228 0.000 0.000
#&gt; ERR519506     2  0.2329     0.0667 0.012 0.916 0.000 0.072
#&gt; ERR519469     3  0.2921     0.7109 0.000 0.000 0.860 0.140
#&gt; ERR519480     3  0.0000     0.8188 0.000 0.000 1.000 0.000
#&gt; ERR519487     3  0.0000     0.8188 0.000 0.000 1.000 0.000
#&gt; ERR519483     2  0.4877     0.6479 0.408 0.592 0.000 0.000
#&gt; ERR519477     2  0.4866     0.6568 0.404 0.596 0.000 0.000
#&gt; ERR519499     3  0.0000     0.8188 0.000 0.000 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-3-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-4'>
<p><a id='tab-ATC-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; ERR519515     1  0.3809      0.557 0.736 0.008 0.000 0.000 0.256
#&gt; ERR519516     1  0.0290      0.893 0.992 0.000 0.000 0.000 0.008
#&gt; ERR519520     4  0.5328      0.231 0.000 0.028 0.468 0.492 0.012
#&gt; ERR519513     3  0.2464      0.825 0.000 0.092 0.892 0.004 0.012
#&gt; ERR519481     4  0.0833      0.676 0.000 0.004 0.016 0.976 0.004
#&gt; ERR519491     5  0.4183      0.549 0.324 0.008 0.000 0.000 0.668
#&gt; ERR519473     4  0.4446      0.445 0.000 0.008 0.400 0.592 0.000
#&gt; ERR519518     3  0.4473      0.386 0.000 0.020 0.656 0.324 0.000
#&gt; ERR519512     4  0.5328      0.231 0.000 0.028 0.468 0.492 0.012
#&gt; ERR519521     4  0.5087      0.517 0.000 0.028 0.344 0.616 0.012
#&gt; ERR519488     1  0.0000      0.892 1.000 0.000 0.000 0.000 0.000
#&gt; ERR519493     5  0.4276      0.497 0.380 0.004 0.000 0.000 0.616
#&gt; ERR519514     1  0.3942      0.541 0.728 0.012 0.000 0.000 0.260
#&gt; ERR519479     4  0.4758      0.342 0.000 0.048 0.000 0.676 0.276
#&gt; ERR519509     1  0.0162      0.892 0.996 0.000 0.000 0.000 0.004
#&gt; ERR519472     4  0.0833      0.676 0.000 0.004 0.016 0.976 0.004
#&gt; ERR519510     5  0.4031      0.496 0.064 0.124 0.000 0.008 0.804
#&gt; ERR519470     1  0.2930      0.720 0.832 0.004 0.000 0.000 0.164
#&gt; ERR519495     4  0.0833      0.676 0.000 0.004 0.016 0.976 0.004
#&gt; ERR519522     4  0.4100      0.678 0.000 0.028 0.172 0.784 0.016
#&gt; ERR519523     4  0.5101      0.512 0.000 0.028 0.348 0.612 0.012
#&gt; ERR519503     2  0.3914      0.696 0.016 0.760 0.220 0.004 0.000
#&gt; ERR519471     1  0.0566      0.887 0.984 0.012 0.000 0.000 0.004
#&gt; ERR519500     4  0.0981      0.669 0.000 0.008 0.012 0.972 0.008
#&gt; ERR519485     1  0.1525      0.865 0.948 0.012 0.000 0.004 0.036
#&gt; ERR519476     1  0.0162      0.893 0.996 0.000 0.000 0.000 0.004
#&gt; ERR519502     4  0.2463      0.705 0.000 0.008 0.100 0.888 0.004
#&gt; ERR519486     5  0.7313      0.243 0.260 0.196 0.044 0.004 0.496
#&gt; ERR519478     5  0.4641      0.316 0.456 0.012 0.000 0.000 0.532
#&gt; ERR519497     3  0.4380      0.582 0.000 0.020 0.728 0.240 0.012
#&gt; ERR519467     4  0.3154      0.704 0.000 0.024 0.104 0.860 0.012
#&gt; ERR519489     4  0.3689      0.630 0.000 0.004 0.256 0.740 0.000
#&gt; ERR519494     3  0.1341      0.850 0.000 0.000 0.944 0.056 0.000
#&gt; ERR519474     1  0.1364      0.868 0.952 0.012 0.000 0.000 0.036
#&gt; ERR519505     2  0.2451      0.697 0.000 0.904 0.056 0.004 0.036
#&gt; ERR519517     3  0.0000      0.875 0.000 0.000 1.000 0.000 0.000
#&gt; ERR519484     5  0.4326      0.491 0.084 0.124 0.000 0.008 0.784
#&gt; ERR519498     3  0.3170      0.789 0.000 0.124 0.848 0.004 0.024
#&gt; ERR519490     3  0.0510      0.873 0.000 0.000 0.984 0.016 0.000
#&gt; ERR519507     4  0.4355      0.422 0.000 0.044 0.000 0.732 0.224
#&gt; ERR519511     5  0.2822      0.507 0.036 0.064 0.000 0.012 0.888
#&gt; ERR519468     3  0.0162      0.876 0.000 0.000 0.996 0.004 0.000
#&gt; ERR519482     3  0.0162      0.876 0.000 0.000 0.996 0.004 0.000
#&gt; ERR519475     1  0.0162      0.893 0.996 0.000 0.000 0.000 0.004
#&gt; ERR519496     5  0.4927      0.447 0.388 0.024 0.000 0.004 0.584
#&gt; ERR519506     2  0.3395      0.605 0.236 0.764 0.000 0.000 0.000
#&gt; ERR519469     3  0.3388      0.676 0.000 0.008 0.792 0.200 0.000
#&gt; ERR519480     3  0.0162      0.876 0.000 0.000 0.996 0.004 0.000
#&gt; ERR519487     3  0.0000      0.875 0.000 0.000 1.000 0.000 0.000
#&gt; ERR519483     1  0.1646      0.862 0.944 0.020 0.000 0.004 0.032
#&gt; ERR519477     1  0.0162      0.893 0.996 0.000 0.000 0.000 0.004
#&gt; ERR519499     3  0.0000      0.875 0.000 0.000 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-4-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-5'>
<p><a id='tab-ATC-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; ERR519515     1  0.3843     -0.092 0.548 0.452 0.000 0.000 0.000 0.000
#&gt; ERR519516     1  0.0547      0.792 0.980 0.020 0.000 0.000 0.000 0.000
#&gt; ERR519520     4  0.4191      0.346 0.000 0.012 0.388 0.596 0.000 0.004
#&gt; ERR519513     3  0.5441      0.628 0.000 0.088 0.716 0.048 0.048 0.100
#&gt; ERR519481     4  0.2793      0.461 0.000 0.000 0.000 0.800 0.200 0.000
#&gt; ERR519491     2  0.5063      0.638 0.284 0.604 0.000 0.000 0.112 0.000
#&gt; ERR519473     4  0.4445      0.382 0.000 0.000 0.396 0.572 0.032 0.000
#&gt; ERR519518     3  0.3966      0.109 0.000 0.000 0.552 0.444 0.000 0.004
#&gt; ERR519512     4  0.4191      0.346 0.000 0.012 0.388 0.596 0.000 0.004
#&gt; ERR519521     4  0.3885      0.505 0.000 0.012 0.300 0.684 0.000 0.004
#&gt; ERR519488     1  0.0458      0.793 0.984 0.016 0.000 0.000 0.000 0.000
#&gt; ERR519493     2  0.5528      0.579 0.348 0.508 0.000 0.000 0.144 0.000
#&gt; ERR519514     1  0.3866     -0.192 0.516 0.484 0.000 0.000 0.000 0.000
#&gt; ERR519479     5  0.4735      0.240 0.000 0.040 0.000 0.416 0.540 0.004
#&gt; ERR519509     1  0.0865      0.784 0.964 0.036 0.000 0.000 0.000 0.000
#&gt; ERR519472     4  0.2730      0.472 0.000 0.000 0.000 0.808 0.192 0.000
#&gt; ERR519510     5  0.4217      0.419 0.016 0.260 0.000 0.000 0.700 0.024
#&gt; ERR519470     1  0.3563      0.284 0.664 0.336 0.000 0.000 0.000 0.000
#&gt; ERR519495     4  0.2793      0.462 0.000 0.000 0.000 0.800 0.200 0.000
#&gt; ERR519522     4  0.3530      0.611 0.000 0.028 0.160 0.800 0.008 0.004
#&gt; ERR519523     4  0.3938      0.491 0.000 0.012 0.312 0.672 0.000 0.004
#&gt; ERR519503     6  0.2257      0.799 0.008 0.000 0.116 0.000 0.000 0.876
#&gt; ERR519471     1  0.1411      0.765 0.936 0.060 0.000 0.000 0.000 0.004
#&gt; ERR519500     4  0.3052      0.439 0.000 0.004 0.000 0.780 0.216 0.000
#&gt; ERR519485     1  0.1895      0.738 0.912 0.072 0.000 0.000 0.016 0.000
#&gt; ERR519476     1  0.0000      0.794 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; ERR519502     4  0.3347      0.580 0.000 0.004 0.068 0.824 0.104 0.000
#&gt; ERR519486     2  0.7545     -0.147 0.180 0.428 0.020 0.000 0.252 0.120
#&gt; ERR519478     2  0.4497      0.586 0.328 0.624 0.000 0.000 0.048 0.000
#&gt; ERR519497     3  0.4226      0.237 0.000 0.012 0.580 0.404 0.000 0.004
#&gt; ERR519467     4  0.3685      0.577 0.000 0.024 0.060 0.832 0.068 0.016
#&gt; ERR519489     4  0.5260      0.452 0.000 0.004 0.348 0.552 0.096 0.000
#&gt; ERR519494     3  0.0713      0.787 0.000 0.000 0.972 0.028 0.000 0.000
#&gt; ERR519474     1  0.1500      0.759 0.936 0.052 0.000 0.000 0.012 0.000
#&gt; ERR519505     6  0.1492      0.792 0.000 0.036 0.000 0.000 0.024 0.940
#&gt; ERR519517     3  0.0000      0.803 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519484     5  0.4455      0.413 0.028 0.248 0.000 0.000 0.696 0.028
#&gt; ERR519498     3  0.6546      0.528 0.000 0.156 0.612 0.064 0.056 0.112
#&gt; ERR519490     3  0.0260      0.800 0.000 0.000 0.992 0.008 0.000 0.000
#&gt; ERR519507     5  0.4664      0.115 0.000 0.032 0.000 0.476 0.488 0.004
#&gt; ERR519511     5  0.4000      0.373 0.008 0.324 0.000 0.000 0.660 0.008
#&gt; ERR519468     3  0.0000      0.803 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519482     3  0.0000      0.803 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519475     1  0.0000      0.794 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; ERR519496     2  0.4939      0.595 0.292 0.612 0.000 0.000 0.096 0.000
#&gt; ERR519506     6  0.2257      0.794 0.116 0.008 0.000 0.000 0.000 0.876
#&gt; ERR519469     3  0.3592      0.376 0.000 0.000 0.656 0.344 0.000 0.000
#&gt; ERR519480     3  0.0000      0.803 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519487     3  0.0000      0.803 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; ERR519483     1  0.1707      0.752 0.928 0.056 0.000 0.000 0.004 0.012
#&gt; ERR519477     1  0.0000      0.794 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; ERR519499     3  0.0000      0.803 0.000 0.000 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-5-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-get-signatures'>
<ul>
<li><a href='#tab-ATC-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-skmeans-signature_compare](figure_cola/ATC-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-skmeans-collect-classes](figure_cola/ATC-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:pam*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "pam"]
# you can also extract it by
# res = res_list["ATC:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 18140 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 5.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-pam-collect-plots](figure_cola/ATC-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-pam-select-partition-number](figure_cola/ATC-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000          0.112 0.889   0.889
#> 3 3 1.000           0.986       0.995          3.951 0.557   0.501
#> 4 4 1.000           0.950       0.983          0.128 0.926   0.834
#> 5 5 0.918           0.874       0.956          0.209 0.807   0.523
#> 6 6 0.878           0.842       0.953          0.019 0.986   0.942
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 5
#> attr(,"optional")
#> [1] 2 3 4
```

There is also optional best $k$ = 2 3 4 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-get-classes'>
<ul>
<li><a href='#tab-ATC-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-pam-get-classes-1'>
<p><a id='tab-ATC-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette p1 p2
#&gt; ERR519515     1       0          1  1  0
#&gt; ERR519516     1       0          1  1  0
#&gt; ERR519520     1       0          1  1  0
#&gt; ERR519513     1       0          1  1  0
#&gt; ERR519481     1       0          1  1  0
#&gt; ERR519491     1       0          1  1  0
#&gt; ERR519473     1       0          1  1  0
#&gt; ERR519518     1       0          1  1  0
#&gt; ERR519512     1       0          1  1  0
#&gt; ERR519521     1       0          1  1  0
#&gt; ERR519488     1       0          1  1  0
#&gt; ERR519493     1       0          1  1  0
#&gt; ERR519514     1       0          1  1  0
#&gt; ERR519479     1       0          1  1  0
#&gt; ERR519509     1       0          1  1  0
#&gt; ERR519472     1       0          1  1  0
#&gt; ERR519510     1       0          1  1  0
#&gt; ERR519470     1       0          1  1  0
#&gt; ERR519495     1       0          1  1  0
#&gt; ERR519522     1       0          1  1  0
#&gt; ERR519523     1       0          1  1  0
#&gt; ERR519503     1       0          1  1  0
#&gt; ERR519471     1       0          1  1  0
#&gt; ERR519500     1       0          1  1  0
#&gt; ERR519485     1       0          1  1  0
#&gt; ERR519476     2       0          1  0  1
#&gt; ERR519502     1       0          1  1  0
#&gt; ERR519486     1       0          1  1  0
#&gt; ERR519478     1       0          1  1  0
#&gt; ERR519497     1       0          1  1  0
#&gt; ERR519467     1       0          1  1  0
#&gt; ERR519489     1       0          1  1  0
#&gt; ERR519494     1       0          1  1  0
#&gt; ERR519474     1       0          1  1  0
#&gt; ERR519505     1       0          1  1  0
#&gt; ERR519517     1       0          1  1  0
#&gt; ERR519484     1       0          1  1  0
#&gt; ERR519498     1       0          1  1  0
#&gt; ERR519490     1       0          1  1  0
#&gt; ERR519507     1       0          1  1  0
#&gt; ERR519511     1       0          1  1  0
#&gt; ERR519468     1       0          1  1  0
#&gt; ERR519482     1       0          1  1  0
#&gt; ERR519475     2       0          1  0  1
#&gt; ERR519496     1       0          1  1  0
#&gt; ERR519506     1       0          1  1  0
#&gt; ERR519469     1       0          1  1  0
#&gt; ERR519480     1       0          1  1  0
#&gt; ERR519487     1       0          1  1  0
#&gt; ERR519483     1       0          1  1  0
#&gt; ERR519477     2       0          1  0  1
#&gt; ERR519499     1       0          1  1  0
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-1-a').click(function(){
  $('#tab-ATC-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-2'>
<p><a id='tab-ATC-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette   p1 p2   p3
#&gt; ERR519515     1   0.000      1.000 1.00  0 0.00
#&gt; ERR519516     1   0.000      1.000 1.00  0 0.00
#&gt; ERR519520     3   0.000      0.983 0.00  0 1.00
#&gt; ERR519513     3   0.000      0.983 0.00  0 1.00
#&gt; ERR519481     3   0.000      0.983 0.00  0 1.00
#&gt; ERR519491     1   0.000      1.000 1.00  0 0.00
#&gt; ERR519473     3   0.000      0.983 0.00  0 1.00
#&gt; ERR519518     3   0.000      0.983 0.00  0 1.00
#&gt; ERR519512     3   0.000      0.983 0.00  0 1.00
#&gt; ERR519521     3   0.000      0.983 0.00  0 1.00
#&gt; ERR519488     1   0.000      1.000 1.00  0 0.00
#&gt; ERR519493     1   0.000      1.000 1.00  0 0.00
#&gt; ERR519514     1   0.000      1.000 1.00  0 0.00
#&gt; ERR519479     1   0.000      1.000 1.00  0 0.00
#&gt; ERR519509     1   0.000      1.000 1.00  0 0.00
#&gt; ERR519472     1   0.000      1.000 1.00  0 0.00
#&gt; ERR519510     1   0.000      1.000 1.00  0 0.00
#&gt; ERR519470     1   0.000      1.000 1.00  0 0.00
#&gt; ERR519495     1   0.000      1.000 1.00  0 0.00
#&gt; ERR519522     3   0.000      0.983 0.00  0 1.00
#&gt; ERR519523     3   0.000      0.983 0.00  0 1.00
#&gt; ERR519503     1   0.000      1.000 1.00  0 0.00
#&gt; ERR519471     1   0.000      1.000 1.00  0 0.00
#&gt; ERR519500     1   0.000      1.000 1.00  0 0.00
#&gt; ERR519485     1   0.000      1.000 1.00  0 0.00
#&gt; ERR519476     2   0.000      1.000 0.00  1 0.00
#&gt; ERR519502     3   0.000      0.983 0.00  0 1.00
#&gt; ERR519486     1   0.000      1.000 1.00  0 0.00
#&gt; ERR519478     1   0.000      1.000 1.00  0 0.00
#&gt; ERR519497     3   0.000      0.983 0.00  0 1.00
#&gt; ERR519467     1   0.000      1.000 1.00  0 0.00
#&gt; ERR519489     3   0.502      0.595 0.24  0 0.76
#&gt; ERR519494     3   0.000      0.983 0.00  0 1.00
#&gt; ERR519474     1   0.000      1.000 1.00  0 0.00
#&gt; ERR519505     1   0.000      1.000 1.00  0 0.00
#&gt; ERR519517     3   0.000      0.983 0.00  0 1.00
#&gt; ERR519484     1   0.000      1.000 1.00  0 0.00
#&gt; ERR519498     1   0.000      1.000 1.00  0 0.00
#&gt; ERR519490     3   0.000      0.983 0.00  0 1.00
#&gt; ERR519507     1   0.000      1.000 1.00  0 0.00
#&gt; ERR519511     1   0.000      1.000 1.00  0 0.00
#&gt; ERR519468     3   0.000      0.983 0.00  0 1.00
#&gt; ERR519482     3   0.000      0.983 0.00  0 1.00
#&gt; ERR519475     2   0.000      1.000 0.00  1 0.00
#&gt; ERR519496     1   0.000      1.000 1.00  0 0.00
#&gt; ERR519506     1   0.000      1.000 1.00  0 0.00
#&gt; ERR519469     3   0.000      0.983 0.00  0 1.00
#&gt; ERR519480     3   0.000      0.983 0.00  0 1.00
#&gt; ERR519487     3   0.000      0.983 0.00  0 1.00
#&gt; ERR519483     1   0.000      1.000 1.00  0 0.00
#&gt; ERR519477     2   0.000      1.000 0.00  1 0.00
#&gt; ERR519499     3   0.000      0.983 0.00  0 1.00
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-2-a').click(function(){
  $('#tab-ATC-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-3'>
<p><a id='tab-ATC-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3    p4
#&gt; ERR519515     1  0.0000     0.9972 1.000  0 0.000 0.000
#&gt; ERR519516     1  0.0000     0.9972 1.000  0 0.000 0.000
#&gt; ERR519520     4  0.0336     0.9686 0.000  0 0.008 0.992
#&gt; ERR519513     4  0.0469     0.9665 0.000  0 0.012 0.988
#&gt; ERR519481     4  0.0000     0.9648 0.000  0 0.000 1.000
#&gt; ERR519491     1  0.0000     0.9972 1.000  0 0.000 0.000
#&gt; ERR519473     4  0.0188     0.9674 0.000  0 0.004 0.996
#&gt; ERR519518     4  0.0336     0.9686 0.000  0 0.008 0.992
#&gt; ERR519512     4  0.0336     0.9686 0.000  0 0.008 0.992
#&gt; ERR519521     4  0.0336     0.9686 0.000  0 0.008 0.992
#&gt; ERR519488     1  0.0000     0.9972 1.000  0 0.000 0.000
#&gt; ERR519493     1  0.0000     0.9972 1.000  0 0.000 0.000
#&gt; ERR519514     1  0.0000     0.9972 1.000  0 0.000 0.000
#&gt; ERR519479     1  0.0336     0.9940 0.992  0 0.000 0.008
#&gt; ERR519509     1  0.0000     0.9972 1.000  0 0.000 0.000
#&gt; ERR519472     1  0.0336     0.9940 0.992  0 0.000 0.008
#&gt; ERR519510     1  0.0000     0.9972 1.000  0 0.000 0.000
#&gt; ERR519470     1  0.0000     0.9972 1.000  0 0.000 0.000
#&gt; ERR519495     1  0.0336     0.9940 0.992  0 0.000 0.008
#&gt; ERR519522     4  0.0188     0.9672 0.000  0 0.004 0.996
#&gt; ERR519523     4  0.0336     0.9686 0.000  0 0.008 0.992
#&gt; ERR519503     1  0.0188     0.9957 0.996  0 0.000 0.004
#&gt; ERR519471     1  0.0000     0.9972 1.000  0 0.000 0.000
#&gt; ERR519500     1  0.0336     0.9940 0.992  0 0.000 0.008
#&gt; ERR519485     1  0.0000     0.9972 1.000  0 0.000 0.000
#&gt; ERR519476     2  0.0000     1.0000 0.000  1 0.000 0.000
#&gt; ERR519502     4  0.0000     0.9648 0.000  0 0.000 1.000
#&gt; ERR519486     1  0.0188     0.9957 0.996  0 0.000 0.004
#&gt; ERR519478     1  0.0000     0.9972 1.000  0 0.000 0.000
#&gt; ERR519497     4  0.0336     0.9686 0.000  0 0.008 0.992
#&gt; ERR519467     1  0.0592     0.9867 0.984  0 0.000 0.016
#&gt; ERR519489     4  0.3837     0.5927 0.224  0 0.000 0.776
#&gt; ERR519494     3  0.4994     0.0753 0.000  0 0.520 0.480
#&gt; ERR519474     1  0.0000     0.9972 1.000  0 0.000 0.000
#&gt; ERR519505     1  0.0336     0.9940 0.992  0 0.000 0.008
#&gt; ERR519517     3  0.0000     0.8817 0.000  0 1.000 0.000
#&gt; ERR519484     1  0.0000     0.9972 1.000  0 0.000 0.000
#&gt; ERR519498     1  0.0376     0.9935 0.992  0 0.004 0.004
#&gt; ERR519490     4  0.0469     0.9662 0.000  0 0.012 0.988
#&gt; ERR519507     1  0.0336     0.9940 0.992  0 0.000 0.008
#&gt; ERR519511     1  0.0000     0.9972 1.000  0 0.000 0.000
#&gt; ERR519468     3  0.0000     0.8817 0.000  0 1.000 0.000
#&gt; ERR519482     3  0.0000     0.8817 0.000  0 1.000 0.000
#&gt; ERR519475     2  0.0000     1.0000 0.000  1 0.000 0.000
#&gt; ERR519496     1  0.0000     0.9972 1.000  0 0.000 0.000
#&gt; ERR519506     1  0.0000     0.9972 1.000  0 0.000 0.000
#&gt; ERR519469     4  0.0188     0.9674 0.000  0 0.004 0.996
#&gt; ERR519480     3  0.0000     0.8817 0.000  0 1.000 0.000
#&gt; ERR519487     3  0.0000     0.8817 0.000  0 1.000 0.000
#&gt; ERR519483     1  0.0000     0.9972 1.000  0 0.000 0.000
#&gt; ERR519477     2  0.0000     1.0000 0.000  1 0.000 0.000
#&gt; ERR519499     3  0.0000     0.8817 0.000  0 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-3-a').click(function(){
  $('#tab-ATC-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-4'>
<p><a id='tab-ATC-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3    p4    p5
#&gt; ERR519515     1  0.0000     0.9572 1.000  0 0.000 0.000 0.000
#&gt; ERR519516     1  0.0000     0.9572 1.000  0 0.000 0.000 0.000
#&gt; ERR519520     5  0.0000     0.9447 0.000  0 0.000 0.000 1.000
#&gt; ERR519513     5  0.0162     0.9424 0.000  0 0.004 0.000 0.996
#&gt; ERR519481     4  0.0162     0.9078 0.000  0 0.000 0.996 0.004
#&gt; ERR519491     1  0.0000     0.9572 1.000  0 0.000 0.000 0.000
#&gt; ERR519473     4  0.3177     0.7135 0.000  0 0.000 0.792 0.208
#&gt; ERR519518     5  0.0000     0.9447 0.000  0 0.000 0.000 1.000
#&gt; ERR519512     5  0.0000     0.9447 0.000  0 0.000 0.000 1.000
#&gt; ERR519521     5  0.0000     0.9447 0.000  0 0.000 0.000 1.000
#&gt; ERR519488     1  0.0000     0.9572 1.000  0 0.000 0.000 0.000
#&gt; ERR519493     1  0.0000     0.9572 1.000  0 0.000 0.000 0.000
#&gt; ERR519514     1  0.0000     0.9572 1.000  0 0.000 0.000 0.000
#&gt; ERR519479     4  0.0162     0.9088 0.004  0 0.000 0.996 0.000
#&gt; ERR519509     1  0.0000     0.9572 1.000  0 0.000 0.000 0.000
#&gt; ERR519472     4  0.0162     0.9088 0.004  0 0.000 0.996 0.000
#&gt; ERR519510     1  0.0000     0.9572 1.000  0 0.000 0.000 0.000
#&gt; ERR519470     1  0.0000     0.9572 1.000  0 0.000 0.000 0.000
#&gt; ERR519495     4  0.0162     0.9088 0.004  0 0.000 0.996 0.000
#&gt; ERR519522     5  0.2852     0.7726 0.000  0 0.000 0.172 0.828
#&gt; ERR519523     5  0.0000     0.9447 0.000  0 0.000 0.000 1.000
#&gt; ERR519503     1  0.4307    -0.0693 0.504  0 0.000 0.496 0.000
#&gt; ERR519471     1  0.0000     0.9572 1.000  0 0.000 0.000 0.000
#&gt; ERR519500     4  0.0162     0.9088 0.004  0 0.000 0.996 0.000
#&gt; ERR519485     1  0.0000     0.9572 1.000  0 0.000 0.000 0.000
#&gt; ERR519476     2  0.0000     1.0000 0.000  1 0.000 0.000 0.000
#&gt; ERR519502     4  0.0162     0.9078 0.000  0 0.000 0.996 0.004
#&gt; ERR519486     1  0.2852     0.7511 0.828  0 0.000 0.172 0.000
#&gt; ERR519478     1  0.0000     0.9572 1.000  0 0.000 0.000 0.000
#&gt; ERR519497     5  0.0000     0.9447 0.000  0 0.000 0.000 1.000
#&gt; ERR519467     4  0.0566     0.9025 0.004  0 0.000 0.984 0.012
#&gt; ERR519489     4  0.0162     0.9078 0.000  0 0.000 0.996 0.004
#&gt; ERR519494     3  0.4306     0.0528 0.000  0 0.508 0.000 0.492
#&gt; ERR519474     1  0.0000     0.9572 1.000  0 0.000 0.000 0.000
#&gt; ERR519505     4  0.3913     0.4647 0.324  0 0.000 0.676 0.000
#&gt; ERR519517     3  0.0000     0.8921 0.000  0 1.000 0.000 0.000
#&gt; ERR519484     1  0.0000     0.9572 1.000  0 0.000 0.000 0.000
#&gt; ERR519498     5  0.3160     0.7511 0.004  0 0.000 0.188 0.808
#&gt; ERR519490     5  0.0162     0.9421 0.000  0 0.004 0.000 0.996
#&gt; ERR519507     4  0.0162     0.9088 0.004  0 0.000 0.996 0.000
#&gt; ERR519511     1  0.0000     0.9572 1.000  0 0.000 0.000 0.000
#&gt; ERR519468     3  0.0000     0.8921 0.000  0 1.000 0.000 0.000
#&gt; ERR519482     3  0.0000     0.8921 0.000  0 1.000 0.000 0.000
#&gt; ERR519475     2  0.0000     1.0000 0.000  1 0.000 0.000 0.000
#&gt; ERR519496     1  0.0000     0.9572 1.000  0 0.000 0.000 0.000
#&gt; ERR519506     1  0.0290     0.9498 0.992  0 0.000 0.008 0.000
#&gt; ERR519469     4  0.2966     0.7435 0.000  0 0.000 0.816 0.184
#&gt; ERR519480     3  0.0000     0.8921 0.000  0 1.000 0.000 0.000
#&gt; ERR519487     3  0.0000     0.8921 0.000  0 1.000 0.000 0.000
#&gt; ERR519483     1  0.0162     0.9536 0.996  0 0.000 0.004 0.000
#&gt; ERR519477     2  0.0000     1.0000 0.000  1 0.000 0.000 0.000
#&gt; ERR519499     3  0.0000     0.8921 0.000  0 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-4-a').click(function(){
  $('#tab-ATC-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-5'>
<p><a id='tab-ATC-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3    p4    p5    p6
#&gt; ERR519515     1  0.0000     0.9410 1.000  0 0.000 0.000 0.000 0.000
#&gt; ERR519516     1  0.0000     0.9410 1.000  0 0.000 0.000 0.000 0.000
#&gt; ERR519520     4  0.0000     0.9407 0.000  0 0.000 1.000 0.000 0.000
#&gt; ERR519513     4  0.0146     0.9382 0.000  0 0.004 0.996 0.000 0.000
#&gt; ERR519481     5  0.0000     0.9050 0.000  0 0.000 0.000 1.000 0.000
#&gt; ERR519491     1  0.0000     0.9410 1.000  0 0.000 0.000 0.000 0.000
#&gt; ERR519473     5  0.2823     0.6905 0.000  0 0.000 0.204 0.796 0.000
#&gt; ERR519518     4  0.0000     0.9407 0.000  0 0.000 1.000 0.000 0.000
#&gt; ERR519512     4  0.0000     0.9407 0.000  0 0.000 1.000 0.000 0.000
#&gt; ERR519521     4  0.0000     0.9407 0.000  0 0.000 1.000 0.000 0.000
#&gt; ERR519488     1  0.0000     0.9410 1.000  0 0.000 0.000 0.000 0.000
#&gt; ERR519493     1  0.0000     0.9410 1.000  0 0.000 0.000 0.000 0.000
#&gt; ERR519514     1  0.0000     0.9410 1.000  0 0.000 0.000 0.000 0.000
#&gt; ERR519479     5  0.0000     0.9050 0.000  0 0.000 0.000 1.000 0.000
#&gt; ERR519509     1  0.0000     0.9410 1.000  0 0.000 0.000 0.000 0.000
#&gt; ERR519472     5  0.0000     0.9050 0.000  0 0.000 0.000 1.000 0.000
#&gt; ERR519510     1  0.0000     0.9410 1.000  0 0.000 0.000 0.000 0.000
#&gt; ERR519470     1  0.0000     0.9410 1.000  0 0.000 0.000 0.000 0.000
#&gt; ERR519495     5  0.0000     0.9050 0.000  0 0.000 0.000 1.000 0.000
#&gt; ERR519522     4  0.2562     0.7513 0.000  0 0.000 0.828 0.172 0.000
#&gt; ERR519523     4  0.0000     0.9407 0.000  0 0.000 1.000 0.000 0.000
#&gt; ERR519503     1  0.3868    -0.0617 0.504  0 0.000 0.000 0.496 0.000
#&gt; ERR519471     1  0.0000     0.9410 1.000  0 0.000 0.000 0.000 0.000
#&gt; ERR519500     5  0.0000     0.9050 0.000  0 0.000 0.000 1.000 0.000
#&gt; ERR519485     1  0.0000     0.9410 1.000  0 0.000 0.000 0.000 0.000
#&gt; ERR519476     2  0.0000     1.0000 0.000  1 0.000 0.000 0.000 0.000
#&gt; ERR519502     5  0.0000     0.9050 0.000  0 0.000 0.000 1.000 0.000
#&gt; ERR519486     1  0.2562     0.7030 0.828  0 0.000 0.000 0.172 0.000
#&gt; ERR519478     1  0.0000     0.9410 1.000  0 0.000 0.000 0.000 0.000
#&gt; ERR519497     4  0.0000     0.9407 0.000  0 0.000 1.000 0.000 0.000
#&gt; ERR519467     5  0.0363     0.8961 0.000  0 0.000 0.012 0.988 0.000
#&gt; ERR519489     5  0.0000     0.9050 0.000  0 0.000 0.000 1.000 0.000
#&gt; ERR519494     3  0.3868     0.0533 0.000  0 0.508 0.492 0.000 0.000
#&gt; ERR519474     1  0.0000     0.9410 1.000  0 0.000 0.000 0.000 0.000
#&gt; ERR519505     5  0.3515     0.3734 0.324  0 0.000 0.000 0.676 0.000
#&gt; ERR519517     3  0.0000     0.8797 0.000  0 1.000 0.000 0.000 0.000
#&gt; ERR519484     1  0.0000     0.9410 1.000  0 0.000 0.000 0.000 0.000
#&gt; ERR519498     4  0.2697     0.7315 0.000  0 0.000 0.812 0.188 0.000
#&gt; ERR519490     4  0.0146     0.9379 0.000  0 0.004 0.996 0.000 0.000
#&gt; ERR519507     5  0.0000     0.9050 0.000  0 0.000 0.000 1.000 0.000
#&gt; ERR519511     1  0.0000     0.9410 1.000  0 0.000 0.000 0.000 0.000
#&gt; ERR519468     3  0.0000     0.8797 0.000  0 1.000 0.000 0.000 0.000
#&gt; ERR519482     3  0.0000     0.8797 0.000  0 1.000 0.000 0.000 0.000
#&gt; ERR519475     2  0.0000     1.0000 0.000  1 0.000 0.000 0.000 0.000
#&gt; ERR519496     1  0.0000     0.9410 1.000  0 0.000 0.000 0.000 0.000
#&gt; ERR519506     6  0.1910     0.0000 0.108  0 0.000 0.000 0.000 0.892
#&gt; ERR519469     5  0.2631     0.7238 0.000  0 0.000 0.180 0.820 0.000
#&gt; ERR519480     3  0.0000     0.8797 0.000  0 1.000 0.000 0.000 0.000
#&gt; ERR519487     3  0.0000     0.8797 0.000  0 1.000 0.000 0.000 0.000
#&gt; ERR519483     1  0.1910     0.8335 0.892  0 0.000 0.000 0.000 0.108
#&gt; ERR519477     2  0.0000     1.0000 0.000  1 0.000 0.000 0.000 0.000
#&gt; ERR519499     3  0.0000     0.8797 0.000  0 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-5-a').click(function(){
  $('#tab-ATC-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-get-signatures'>
<ul>
<li><a href='#tab-ATC-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-1-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-1"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-2-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-2"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-3-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-3"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-4-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-4"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-5-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-pam-signature_compare](figure_cola/ATC-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-pam-collect-classes](figure_cola/ATC-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:mclust






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "mclust"]
# you can also extract it by
# res = res_list["ATC:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 18140 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 4.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-mclust-collect-plots](figure_cola/ATC-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-mclust-select-partition-number](figure_cola/ATC-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.743           0.929       0.957          0.291 0.708   0.708
#> 3 3 0.481           0.755       0.879          0.562 0.882   0.837
#> 4 4 0.570           0.854       0.872          0.455 0.643   0.444
#> 5 5 0.659           0.504       0.756          0.043 0.686   0.331
#> 6 6 0.639           0.576       0.779          0.126 0.783   0.421
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 4
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-get-classes'>
<ul>
<li><a href='#tab-ATC-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-mclust-get-classes-1'>
<p><a id='tab-ATC-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; ERR519515     1  0.0000      0.970 1.000 0.000
#&gt; ERR519516     1  0.0000      0.970 1.000 0.000
#&gt; ERR519520     1  0.0000      0.970 1.000 0.000
#&gt; ERR519513     1  0.6148      0.825 0.848 0.152
#&gt; ERR519481     1  0.0000      0.970 1.000 0.000
#&gt; ERR519491     1  0.0000      0.970 1.000 0.000
#&gt; ERR519473     1  0.1414      0.959 0.980 0.020
#&gt; ERR519518     1  0.1414      0.959 0.980 0.020
#&gt; ERR519512     1  0.0000      0.970 1.000 0.000
#&gt; ERR519521     1  0.0000      0.970 1.000 0.000
#&gt; ERR519488     1  0.0000      0.970 1.000 0.000
#&gt; ERR519493     1  0.0000      0.970 1.000 0.000
#&gt; ERR519514     1  0.0000      0.970 1.000 0.000
#&gt; ERR519479     1  0.0000      0.970 1.000 0.000
#&gt; ERR519509     1  0.0000      0.970 1.000 0.000
#&gt; ERR519472     1  0.0000      0.970 1.000 0.000
#&gt; ERR519510     1  0.0000      0.970 1.000 0.000
#&gt; ERR519470     1  0.0000      0.970 1.000 0.000
#&gt; ERR519495     1  0.0000      0.970 1.000 0.000
#&gt; ERR519522     1  0.0000      0.970 1.000 0.000
#&gt; ERR519523     1  0.0000      0.970 1.000 0.000
#&gt; ERR519503     1  0.5629      0.858 0.868 0.132
#&gt; ERR519471     1  0.1414      0.959 0.980 0.020
#&gt; ERR519500     1  0.0000      0.970 1.000 0.000
#&gt; ERR519485     1  0.0672      0.966 0.992 0.008
#&gt; ERR519476     2  0.0000      0.867 0.000 1.000
#&gt; ERR519502     1  0.0000      0.970 1.000 0.000
#&gt; ERR519486     1  0.0376      0.968 0.996 0.004
#&gt; ERR519478     1  0.0000      0.970 1.000 0.000
#&gt; ERR519497     1  0.0938      0.964 0.988 0.012
#&gt; ERR519467     1  0.0000      0.970 1.000 0.000
#&gt; ERR519489     1  0.0000      0.970 1.000 0.000
#&gt; ERR519494     1  0.3114      0.931 0.944 0.056
#&gt; ERR519474     1  0.0000      0.970 1.000 0.000
#&gt; ERR519505     1  0.3584      0.923 0.932 0.068
#&gt; ERR519517     2  0.5629      0.894 0.132 0.868
#&gt; ERR519484     1  0.0000      0.970 1.000 0.000
#&gt; ERR519498     1  0.1633      0.956 0.976 0.024
#&gt; ERR519490     1  0.3274      0.927 0.940 0.060
#&gt; ERR519507     1  0.0000      0.970 1.000 0.000
#&gt; ERR519511     1  0.0000      0.970 1.000 0.000
#&gt; ERR519468     2  0.8016      0.800 0.244 0.756
#&gt; ERR519482     2  0.8386      0.768 0.268 0.732
#&gt; ERR519475     2  0.0000      0.867 0.000 1.000
#&gt; ERR519496     1  0.0000      0.970 1.000 0.000
#&gt; ERR519506     1  0.8555      0.624 0.720 0.280
#&gt; ERR519469     1  0.4022      0.912 0.920 0.080
#&gt; ERR519480     2  0.4690      0.892 0.100 0.900
#&gt; ERR519487     2  0.6148      0.889 0.152 0.848
#&gt; ERR519483     1  0.7950      0.689 0.760 0.240
#&gt; ERR519477     2  0.0000      0.867 0.000 1.000
#&gt; ERR519499     2  0.6148      0.889 0.152 0.848
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-1-a').click(function(){
  $('#tab-ATC-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-2'>
<p><a id='tab-ATC-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; ERR519515     1  0.0000    0.84038 1.000 0.000 0.000
#&gt; ERR519516     1  0.0000    0.84038 1.000 0.000 0.000
#&gt; ERR519520     1  0.5363    0.71673 0.724 0.000 0.276
#&gt; ERR519513     1  0.6925    0.31026 0.532 0.016 0.452
#&gt; ERR519481     1  0.4121    0.79467 0.832 0.000 0.168
#&gt; ERR519491     1  0.0237    0.83987 0.996 0.000 0.004
#&gt; ERR519473     1  0.5785    0.64788 0.668 0.000 0.332
#&gt; ERR519518     1  0.5785    0.64788 0.668 0.000 0.332
#&gt; ERR519512     1  0.5465    0.70416 0.712 0.000 0.288
#&gt; ERR519521     1  0.5397    0.71284 0.720 0.000 0.280
#&gt; ERR519488     1  0.0000    0.84038 1.000 0.000 0.000
#&gt; ERR519493     1  0.0000    0.84038 1.000 0.000 0.000
#&gt; ERR519514     1  0.0000    0.84038 1.000 0.000 0.000
#&gt; ERR519479     1  0.0000    0.84038 1.000 0.000 0.000
#&gt; ERR519509     1  0.0000    0.84038 1.000 0.000 0.000
#&gt; ERR519472     1  0.4887    0.76420 0.772 0.000 0.228
#&gt; ERR519510     1  0.0000    0.84038 1.000 0.000 0.000
#&gt; ERR519470     1  0.0000    0.84038 1.000 0.000 0.000
#&gt; ERR519495     1  0.3879    0.80046 0.848 0.000 0.152
#&gt; ERR519522     1  0.4235    0.79395 0.824 0.000 0.176
#&gt; ERR519523     1  0.5465    0.70416 0.712 0.000 0.288
#&gt; ERR519503     1  0.7184    0.00189 0.504 0.024 0.472
#&gt; ERR519471     1  0.0424    0.83939 0.992 0.000 0.008
#&gt; ERR519500     1  0.4702    0.77612 0.788 0.000 0.212
#&gt; ERR519485     1  0.0000    0.84038 1.000 0.000 0.000
#&gt; ERR519476     2  0.0000    1.00000 0.000 1.000 0.000
#&gt; ERR519502     1  0.4750    0.77101 0.784 0.000 0.216
#&gt; ERR519486     1  0.0000    0.84038 1.000 0.000 0.000
#&gt; ERR519478     1  0.0000    0.84038 1.000 0.000 0.000
#&gt; ERR519497     1  0.4750    0.77101 0.784 0.000 0.216
#&gt; ERR519467     1  0.3619    0.80766 0.864 0.000 0.136
#&gt; ERR519489     1  0.4887    0.76417 0.772 0.000 0.228
#&gt; ERR519494     3  0.4399    0.58510 0.188 0.000 0.812
#&gt; ERR519474     1  0.0000    0.84038 1.000 0.000 0.000
#&gt; ERR519505     1  0.5656    0.53555 0.728 0.008 0.264
#&gt; ERR519517     3  0.2261    0.81728 0.000 0.068 0.932
#&gt; ERR519484     1  0.0000    0.84038 1.000 0.000 0.000
#&gt; ERR519498     1  0.4033    0.80788 0.856 0.008 0.136
#&gt; ERR519490     3  0.0237    0.80896 0.004 0.000 0.996
#&gt; ERR519507     1  0.0237    0.83987 0.996 0.000 0.004
#&gt; ERR519511     1  0.0000    0.84038 1.000 0.000 0.000
#&gt; ERR519468     3  0.2165    0.82030 0.000 0.064 0.936
#&gt; ERR519482     3  0.2165    0.82030 0.000 0.064 0.936
#&gt; ERR519475     2  0.0000    1.00000 0.000 1.000 0.000
#&gt; ERR519496     1  0.0000    0.84038 1.000 0.000 0.000
#&gt; ERR519506     1  0.7112    0.12958 0.552 0.024 0.424
#&gt; ERR519469     3  0.6229    0.21946 0.340 0.008 0.652
#&gt; ERR519480     3  0.1643    0.82188 0.000 0.044 0.956
#&gt; ERR519487     3  0.2537    0.80786 0.000 0.080 0.920
#&gt; ERR519483     1  0.2383    0.81166 0.940 0.044 0.016
#&gt; ERR519477     2  0.0000    1.00000 0.000 1.000 0.000
#&gt; ERR519499     3  0.0592    0.81452 0.000 0.012 0.988
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-2-a').click(function(){
  $('#tab-ATC-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-3'>
<p><a id='tab-ATC-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; ERR519515     1  0.0000      0.940 1.000 0.000 0.000 0.000
#&gt; ERR519516     1  0.0000      0.940 1.000 0.000 0.000 0.000
#&gt; ERR519520     4  0.5462      0.880 0.152 0.000 0.112 0.736
#&gt; ERR519513     3  0.5977      0.135 0.040 0.000 0.528 0.432
#&gt; ERR519481     4  0.3172      0.920 0.160 0.000 0.000 0.840
#&gt; ERR519491     1  0.0000      0.940 1.000 0.000 0.000 0.000
#&gt; ERR519473     4  0.5416      0.878 0.148 0.000 0.112 0.740
#&gt; ERR519518     3  0.7113      0.058 0.152 0.000 0.532 0.316
#&gt; ERR519512     4  0.5462      0.880 0.152 0.000 0.112 0.736
#&gt; ERR519521     4  0.5462      0.880 0.152 0.000 0.112 0.736
#&gt; ERR519488     1  0.0000      0.940 1.000 0.000 0.000 0.000
#&gt; ERR519493     1  0.0000      0.940 1.000 0.000 0.000 0.000
#&gt; ERR519514     1  0.0000      0.940 1.000 0.000 0.000 0.000
#&gt; ERR519479     4  0.3172      0.920 0.160 0.000 0.000 0.840
#&gt; ERR519509     1  0.0000      0.940 1.000 0.000 0.000 0.000
#&gt; ERR519472     4  0.3172      0.920 0.160 0.000 0.000 0.840
#&gt; ERR519510     1  0.0000      0.940 1.000 0.000 0.000 0.000
#&gt; ERR519470     1  0.0000      0.940 1.000 0.000 0.000 0.000
#&gt; ERR519495     4  0.3172      0.920 0.160 0.000 0.000 0.840
#&gt; ERR519522     4  0.3172      0.920 0.160 0.000 0.000 0.840
#&gt; ERR519523     4  0.5462      0.880 0.152 0.000 0.112 0.736
#&gt; ERR519503     1  0.5618      0.635 0.668 0.004 0.040 0.288
#&gt; ERR519471     1  0.0000      0.940 1.000 0.000 0.000 0.000
#&gt; ERR519500     4  0.3172      0.920 0.160 0.000 0.000 0.840
#&gt; ERR519485     1  0.0000      0.940 1.000 0.000 0.000 0.000
#&gt; ERR519476     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; ERR519502     4  0.3172      0.920 0.160 0.000 0.000 0.840
#&gt; ERR519486     1  0.1211      0.910 0.960 0.000 0.000 0.040
#&gt; ERR519478     1  0.1118      0.909 0.964 0.000 0.000 0.036
#&gt; ERR519497     4  0.5462      0.880 0.152 0.000 0.112 0.736
#&gt; ERR519467     4  0.3172      0.920 0.160 0.000 0.000 0.840
#&gt; ERR519489     4  0.3172      0.920 0.160 0.000 0.000 0.840
#&gt; ERR519494     3  0.1388      0.806 0.028 0.000 0.960 0.012
#&gt; ERR519474     1  0.0000      0.940 1.000 0.000 0.000 0.000
#&gt; ERR519505     1  0.5530      0.566 0.616 0.004 0.020 0.360
#&gt; ERR519517     3  0.0000      0.838 0.000 0.000 1.000 0.000
#&gt; ERR519484     1  0.0000      0.940 1.000 0.000 0.000 0.000
#&gt; ERR519498     4  0.4410      0.748 0.064 0.000 0.128 0.808
#&gt; ERR519490     3  0.0336      0.834 0.000 0.000 0.992 0.008
#&gt; ERR519507     4  0.3172      0.920 0.160 0.000 0.000 0.840
#&gt; ERR519511     1  0.0188      0.937 0.996 0.000 0.000 0.004
#&gt; ERR519468     3  0.0000      0.838 0.000 0.000 1.000 0.000
#&gt; ERR519482     3  0.0000      0.838 0.000 0.000 1.000 0.000
#&gt; ERR519475     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; ERR519496     1  0.0188      0.937 0.996 0.000 0.000 0.004
#&gt; ERR519506     1  0.4513      0.738 0.796 0.004 0.040 0.160
#&gt; ERR519469     4  0.3377      0.680 0.012 0.000 0.140 0.848
#&gt; ERR519480     3  0.0000      0.838 0.000 0.000 1.000 0.000
#&gt; ERR519487     3  0.0000      0.838 0.000 0.000 1.000 0.000
#&gt; ERR519483     1  0.3105      0.773 0.856 0.004 0.140 0.000
#&gt; ERR519477     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; ERR519499     3  0.0000      0.838 0.000 0.000 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-3-a').click(function(){
  $('#tab-ATC-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-4'>
<p><a id='tab-ATC-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; ERR519515     1  0.0000     0.6850 1.000 0.000 0.000 0.000 0.000
#&gt; ERR519516     1  0.0000     0.6850 1.000 0.000 0.000 0.000 0.000
#&gt; ERR519520     1  0.5513     0.4389 0.524 0.408 0.068 0.000 0.000
#&gt; ERR519513     5  0.3318     0.4949 0.000 0.000 0.192 0.008 0.800
#&gt; ERR519481     1  0.4297     0.4608 0.528 0.472 0.000 0.000 0.000
#&gt; ERR519491     1  0.0000     0.6850 1.000 0.000 0.000 0.000 0.000
#&gt; ERR519473     4  0.5519     0.5292 0.000 0.412 0.068 0.520 0.000
#&gt; ERR519518     4  0.5892     0.5560 0.000 0.372 0.108 0.520 0.000
#&gt; ERR519512     1  0.5513     0.4389 0.524 0.408 0.068 0.000 0.000
#&gt; ERR519521     1  0.5513     0.4389 0.524 0.408 0.068 0.000 0.000
#&gt; ERR519488     1  0.0162     0.6811 0.996 0.000 0.000 0.000 0.004
#&gt; ERR519493     1  0.0000     0.6850 1.000 0.000 0.000 0.000 0.000
#&gt; ERR519514     1  0.0000     0.6850 1.000 0.000 0.000 0.000 0.000
#&gt; ERR519479     1  0.4291     0.4681 0.536 0.464 0.000 0.000 0.000
#&gt; ERR519509     1  0.0000     0.6850 1.000 0.000 0.000 0.000 0.000
#&gt; ERR519472     2  0.5238    -0.4920 0.476 0.480 0.000 0.044 0.000
#&gt; ERR519510     1  0.0000     0.6850 1.000 0.000 0.000 0.000 0.000
#&gt; ERR519470     1  0.0000     0.6850 1.000 0.000 0.000 0.000 0.000
#&gt; ERR519495     1  0.4297     0.4608 0.528 0.472 0.000 0.000 0.000
#&gt; ERR519522     1  0.4291     0.4681 0.536 0.464 0.000 0.000 0.000
#&gt; ERR519523     1  0.5513     0.4389 0.524 0.408 0.068 0.000 0.000
#&gt; ERR519503     4  0.7532     0.1752 0.120 0.156 0.000 0.516 0.208
#&gt; ERR519471     1  0.1908     0.5757 0.908 0.000 0.000 0.092 0.000
#&gt; ERR519500     1  0.4302     0.4508 0.520 0.480 0.000 0.000 0.000
#&gt; ERR519485     5  0.4302     0.4443 0.480 0.000 0.000 0.000 0.520
#&gt; ERR519476     2  0.4302     0.1415 0.000 0.520 0.000 0.480 0.000
#&gt; ERR519502     1  0.4300     0.4557 0.524 0.476 0.000 0.000 0.000
#&gt; ERR519486     5  0.4898     0.5748 0.248 0.068 0.000 0.000 0.684
#&gt; ERR519478     1  0.0000     0.6850 1.000 0.000 0.000 0.000 0.000
#&gt; ERR519497     2  0.7653    -0.3634 0.160 0.408 0.068 0.360 0.004
#&gt; ERR519467     1  0.4297     0.4608 0.528 0.472 0.000 0.000 0.000
#&gt; ERR519489     2  0.6556    -0.1471 0.260 0.476 0.000 0.264 0.000
#&gt; ERR519494     4  0.5216     0.2789 0.000 0.044 0.436 0.520 0.000
#&gt; ERR519474     1  0.0000     0.6850 1.000 0.000 0.000 0.000 0.000
#&gt; ERR519505     5  0.5470     0.3482 0.008 0.080 0.000 0.272 0.640
#&gt; ERR519517     3  0.0000     1.0000 0.000 0.000 1.000 0.000 0.000
#&gt; ERR519484     1  0.0000     0.6850 1.000 0.000 0.000 0.000 0.000
#&gt; ERR519498     5  0.4218     0.5214 0.000 0.112 0.024 0.060 0.804
#&gt; ERR519490     4  0.4307     0.0984 0.000 0.000 0.500 0.500 0.000
#&gt; ERR519507     1  0.4291     0.4681 0.536 0.464 0.000 0.000 0.000
#&gt; ERR519511     1  0.0000     0.6850 1.000 0.000 0.000 0.000 0.000
#&gt; ERR519468     3  0.0000     1.0000 0.000 0.000 1.000 0.000 0.000
#&gt; ERR519482     3  0.0000     1.0000 0.000 0.000 1.000 0.000 0.000
#&gt; ERR519475     2  0.4302     0.1415 0.000 0.520 0.000 0.480 0.000
#&gt; ERR519496     1  0.0000     0.6850 1.000 0.000 0.000 0.000 0.000
#&gt; ERR519506     5  0.6824     0.0935 0.188 0.012 0.000 0.372 0.428
#&gt; ERR519469     4  0.4650     0.4803 0.000 0.468 0.012 0.520 0.000
#&gt; ERR519480     3  0.0000     1.0000 0.000 0.000 1.000 0.000 0.000
#&gt; ERR519487     3  0.0000     1.0000 0.000 0.000 1.000 0.000 0.000
#&gt; ERR519483     5  0.5094     0.5987 0.220 0.000 0.076 0.008 0.696
#&gt; ERR519477     2  0.4302     0.1415 0.000 0.520 0.000 0.480 0.000
#&gt; ERR519499     3  0.0000     1.0000 0.000 0.000 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-4-a').click(function(){
  $('#tab-ATC-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-5'>
<p><a id='tab-ATC-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3    p4    p5    p6
#&gt; ERR519515     1  0.2980     0.7235 0.800  0 0.000 0.008 0.192 0.000
#&gt; ERR519516     1  0.3144     0.5980 0.808  0 0.000 0.172 0.016 0.004
#&gt; ERR519520     5  0.4172     0.3577 0.008  0 0.008 0.376 0.608 0.000
#&gt; ERR519513     6  0.2664     0.4329 0.000  0 0.184 0.000 0.000 0.816
#&gt; ERR519481     5  0.0547     0.7324 0.020  0 0.000 0.000 0.980 0.000
#&gt; ERR519491     1  0.2823     0.7199 0.796  0 0.000 0.000 0.204 0.000
#&gt; ERR519473     4  0.3758     0.4724 0.000  0 0.008 0.668 0.324 0.000
#&gt; ERR519518     4  0.4408     0.5064 0.000  0 0.056 0.664 0.280 0.000
#&gt; ERR519512     5  0.4274     0.3418 0.012  0 0.008 0.380 0.600 0.000
#&gt; ERR519521     5  0.4264     0.3604 0.012  0 0.008 0.376 0.604 0.000
#&gt; ERR519488     1  0.2955     0.5910 0.816  0 0.000 0.172 0.008 0.004
#&gt; ERR519493     1  0.2823     0.7199 0.796  0 0.000 0.000 0.204 0.000
#&gt; ERR519514     1  0.2793     0.7212 0.800  0 0.000 0.000 0.200 0.000
#&gt; ERR519479     5  0.2823     0.5605 0.204  0 0.000 0.000 0.796 0.000
#&gt; ERR519509     1  0.4403     0.6381 0.724  0 0.000 0.172 0.100 0.004
#&gt; ERR519472     5  0.0603     0.7176 0.004  0 0.000 0.016 0.980 0.000
#&gt; ERR519510     1  0.0260     0.6817 0.992  0 0.000 0.000 0.008 0.000
#&gt; ERR519470     1  0.3485     0.7201 0.772  0 0.000 0.020 0.204 0.004
#&gt; ERR519495     5  0.0547     0.7324 0.020  0 0.000 0.000 0.980 0.000
#&gt; ERR519522     5  0.0547     0.7324 0.020  0 0.000 0.000 0.980 0.000
#&gt; ERR519523     5  0.4172     0.3577 0.008  0 0.008 0.376 0.608 0.000
#&gt; ERR519503     4  0.6416    -0.1282 0.384  0 0.000 0.444 0.080 0.092
#&gt; ERR519471     1  0.1462     0.6571 0.936  0 0.000 0.056 0.008 0.000
#&gt; ERR519500     5  0.0865     0.7232 0.036  0 0.000 0.000 0.964 0.000
#&gt; ERR519485     1  0.5173     0.3258 0.636  0 0.000 0.172 0.004 0.188
#&gt; ERR519476     2  0.0000     1.0000 0.000  1 0.000 0.000 0.000 0.000
#&gt; ERR519502     5  0.0363     0.7290 0.012  0 0.000 0.000 0.988 0.000
#&gt; ERR519486     1  0.4503     0.3365 0.696  0 0.000 0.000 0.100 0.204
#&gt; ERR519478     1  0.3198     0.6788 0.740  0 0.000 0.000 0.260 0.000
#&gt; ERR519497     4  0.4658     0.4286 0.040  0 0.008 0.612 0.340 0.000
#&gt; ERR519467     5  0.0547     0.7324 0.020  0 0.000 0.000 0.980 0.000
#&gt; ERR519489     5  0.3373     0.2945 0.008  0 0.000 0.248 0.744 0.000
#&gt; ERR519494     4  0.4294    -0.1528 0.000  0 0.428 0.552 0.020 0.000
#&gt; ERR519474     1  0.2810     0.6037 0.832  0 0.000 0.156 0.008 0.004
#&gt; ERR519505     6  0.6073     0.3677 0.088  0 0.000 0.228 0.096 0.588
#&gt; ERR519517     3  0.0000     0.9033 0.000  0 1.000 0.000 0.000 0.000
#&gt; ERR519484     1  0.0260     0.6817 0.992  0 0.000 0.000 0.008 0.000
#&gt; ERR519498     6  0.3529     0.4751 0.000  0 0.016 0.048 0.120 0.816
#&gt; ERR519490     3  0.3864     0.1293 0.000  0 0.520 0.480 0.000 0.000
#&gt; ERR519507     5  0.2762     0.5695 0.196  0 0.000 0.000 0.804 0.000
#&gt; ERR519511     1  0.3330     0.6558 0.716  0 0.000 0.000 0.284 0.000
#&gt; ERR519468     3  0.0000     0.9033 0.000  0 1.000 0.000 0.000 0.000
#&gt; ERR519482     3  0.0000     0.9033 0.000  0 1.000 0.000 0.000 0.000
#&gt; ERR519475     2  0.0000     1.0000 0.000  1 0.000 0.000 0.000 0.000
#&gt; ERR519496     1  0.2941     0.7113 0.780  0 0.000 0.000 0.220 0.000
#&gt; ERR519506     1  0.6122    -0.0615 0.396  0 0.000 0.392 0.008 0.204
#&gt; ERR519469     4  0.3023     0.5094 0.000  0 0.000 0.768 0.232 0.000
#&gt; ERR519480     3  0.0000     0.9033 0.000  0 1.000 0.000 0.000 0.000
#&gt; ERR519487     3  0.0000     0.9033 0.000  0 1.000 0.000 0.000 0.000
#&gt; ERR519483     6  0.6001    -0.1586 0.392  0 0.008 0.176 0.000 0.424
#&gt; ERR519477     2  0.0000     1.0000 0.000  1 0.000 0.000 0.000 0.000
#&gt; ERR519499     3  0.0000     0.9033 0.000  0 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-5-a').click(function(){
  $('#tab-ATC-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-get-signatures'>
<ul>
<li><a href='#tab-ATC-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-1-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-1"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-2-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-2"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-3-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-3"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-4-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-4"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-5-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-mclust-signature_compare](figure_cola/ATC-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-mclust-collect-classes](figure_cola/ATC-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:NMF






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "NMF"]
# you can also extract it by
# res = res_list["ATC:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 18140 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-NMF-collect-plots](figure_cola/ATC-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-NMF-select-partition-number](figure_cola/ATC-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.633           0.810       0.915         0.4764 0.502   0.502
#> 3 3 0.407           0.633       0.790         0.3014 0.813   0.645
#> 4 4 0.365           0.510       0.730         0.1116 0.865   0.664
#> 5 5 0.388           0.386       0.615         0.0599 0.918   0.762
#> 6 6 0.423           0.375       0.595         0.0781 0.814   0.460
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-get-classes'>
<ul>
<li><a href='#tab-ATC-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-NMF-get-classes-1'>
<p><a id='tab-ATC-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; ERR519515     1  0.0000      0.936 1.000 0.000
#&gt; ERR519516     1  0.0000      0.936 1.000 0.000
#&gt; ERR519520     1  0.7883      0.680 0.764 0.236
#&gt; ERR519513     2  0.0672      0.853 0.008 0.992
#&gt; ERR519481     1  0.0376      0.935 0.996 0.004
#&gt; ERR519491     1  0.0000      0.936 1.000 0.000
#&gt; ERR519473     2  0.5629      0.791 0.132 0.868
#&gt; ERR519518     2  0.2778      0.840 0.048 0.952
#&gt; ERR519512     1  0.9580      0.333 0.620 0.380
#&gt; ERR519521     1  0.1414      0.927 0.980 0.020
#&gt; ERR519488     1  0.0000      0.936 1.000 0.000
#&gt; ERR519493     1  0.0000      0.936 1.000 0.000
#&gt; ERR519514     1  0.0672      0.933 0.992 0.008
#&gt; ERR519479     1  0.0000      0.936 1.000 0.000
#&gt; ERR519509     1  0.0000      0.936 1.000 0.000
#&gt; ERR519472     1  0.8207      0.644 0.744 0.256
#&gt; ERR519510     1  0.0000      0.936 1.000 0.000
#&gt; ERR519470     1  0.0000      0.936 1.000 0.000
#&gt; ERR519495     1  0.0376      0.935 0.996 0.004
#&gt; ERR519522     1  0.0000      0.936 1.000 0.000
#&gt; ERR519523     1  0.3584      0.890 0.932 0.068
#&gt; ERR519503     2  0.0376      0.853 0.004 0.996
#&gt; ERR519471     1  0.7950      0.673 0.760 0.240
#&gt; ERR519500     1  0.2236      0.917 0.964 0.036
#&gt; ERR519485     1  0.0000      0.936 1.000 0.000
#&gt; ERR519476     2  0.9993      0.197 0.484 0.516
#&gt; ERR519502     1  0.7453      0.719 0.788 0.212
#&gt; ERR519486     1  0.3879      0.882 0.924 0.076
#&gt; ERR519478     1  0.0000      0.936 1.000 0.000
#&gt; ERR519497     2  0.8144      0.680 0.252 0.748
#&gt; ERR519467     1  0.0000      0.936 1.000 0.000
#&gt; ERR519489     2  0.8327      0.664 0.264 0.736
#&gt; ERR519494     2  0.0376      0.853 0.004 0.996
#&gt; ERR519474     1  0.0000      0.936 1.000 0.000
#&gt; ERR519505     2  0.9358      0.510 0.352 0.648
#&gt; ERR519517     2  0.0000      0.852 0.000 1.000
#&gt; ERR519484     1  0.0938      0.932 0.988 0.012
#&gt; ERR519498     2  0.8386      0.659 0.268 0.732
#&gt; ERR519490     2  0.0000      0.852 0.000 1.000
#&gt; ERR519507     1  0.0376      0.935 0.996 0.004
#&gt; ERR519511     1  0.0000      0.936 1.000 0.000
#&gt; ERR519468     2  0.0000      0.852 0.000 1.000
#&gt; ERR519482     2  0.0000      0.852 0.000 1.000
#&gt; ERR519475     2  0.9993      0.197 0.484 0.516
#&gt; ERR519496     1  0.0672      0.933 0.992 0.008
#&gt; ERR519506     2  0.1184      0.852 0.016 0.984
#&gt; ERR519469     2  0.1184      0.851 0.016 0.984
#&gt; ERR519480     2  0.0000      0.852 0.000 1.000
#&gt; ERR519487     2  0.0000      0.852 0.000 1.000
#&gt; ERR519483     2  0.2043      0.847 0.032 0.968
#&gt; ERR519477     2  0.9993      0.197 0.484 0.516
#&gt; ERR519499     2  0.0000      0.852 0.000 1.000
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-1-a').click(function(){
  $('#tab-ATC-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-2'>
<p><a id='tab-ATC-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; ERR519515     1  0.1860      0.826 0.948 0.052 0.000
#&gt; ERR519516     1  0.3192      0.786 0.888 0.112 0.000
#&gt; ERR519520     1  0.6100      0.701 0.784 0.120 0.096
#&gt; ERR519513     2  0.6744      0.325 0.032 0.668 0.300
#&gt; ERR519481     1  0.2945      0.800 0.908 0.088 0.004
#&gt; ERR519491     1  0.2625      0.809 0.916 0.084 0.000
#&gt; ERR519473     3  0.7085      0.624 0.096 0.188 0.716
#&gt; ERR519518     3  0.3502      0.776 0.020 0.084 0.896
#&gt; ERR519512     1  0.8532      0.352 0.608 0.168 0.224
#&gt; ERR519521     1  0.2229      0.833 0.944 0.044 0.012
#&gt; ERR519488     1  0.4504      0.702 0.804 0.196 0.000
#&gt; ERR519493     1  0.1860      0.829 0.948 0.052 0.000
#&gt; ERR519514     1  0.0592      0.835 0.988 0.012 0.000
#&gt; ERR519479     1  0.1163      0.833 0.972 0.028 0.000
#&gt; ERR519509     1  0.2537      0.812 0.920 0.080 0.000
#&gt; ERR519472     1  0.8482      0.420 0.616 0.200 0.184
#&gt; ERR519510     1  0.4399      0.698 0.812 0.188 0.000
#&gt; ERR519470     1  0.1753      0.834 0.952 0.048 0.000
#&gt; ERR519495     1  0.3030      0.798 0.904 0.092 0.004
#&gt; ERR519522     1  0.2066      0.825 0.940 0.060 0.000
#&gt; ERR519523     1  0.2492      0.825 0.936 0.048 0.016
#&gt; ERR519503     3  0.4784      0.733 0.004 0.200 0.796
#&gt; ERR519471     1  0.7509      0.423 0.636 0.300 0.064
#&gt; ERR519500     1  0.5692      0.681 0.784 0.176 0.040
#&gt; ERR519485     2  0.5835      0.460 0.340 0.660 0.000
#&gt; ERR519476     2  0.9998      0.298 0.328 0.344 0.328
#&gt; ERR519502     1  0.7672      0.544 0.684 0.156 0.160
#&gt; ERR519486     2  0.6224      0.509 0.296 0.688 0.016
#&gt; ERR519478     1  0.1163      0.835 0.972 0.028 0.000
#&gt; ERR519497     3  0.9215      0.120 0.168 0.332 0.500
#&gt; ERR519467     1  0.2096      0.830 0.944 0.052 0.004
#&gt; ERR519489     3  0.8792      0.358 0.244 0.176 0.580
#&gt; ERR519494     3  0.4136      0.755 0.020 0.116 0.864
#&gt; ERR519474     2  0.6274      0.240 0.456 0.544 0.000
#&gt; ERR519505     2  0.8055      0.336 0.096 0.612 0.292
#&gt; ERR519517     3  0.2796      0.779 0.000 0.092 0.908
#&gt; ERR519484     2  0.6307      0.148 0.488 0.512 0.000
#&gt; ERR519498     2  0.7047      0.451 0.084 0.712 0.204
#&gt; ERR519490     3  0.1163      0.794 0.000 0.028 0.972
#&gt; ERR519507     1  0.1525      0.834 0.964 0.032 0.004
#&gt; ERR519511     1  0.1753      0.827 0.952 0.048 0.000
#&gt; ERR519468     3  0.3267      0.771 0.000 0.116 0.884
#&gt; ERR519482     3  0.3482      0.766 0.000 0.128 0.872
#&gt; ERR519475     2  0.9998      0.298 0.328 0.344 0.328
#&gt; ERR519496     1  0.1753      0.833 0.952 0.048 0.000
#&gt; ERR519506     2  0.7271      0.184 0.040 0.608 0.352
#&gt; ERR519469     3  0.4068      0.758 0.016 0.120 0.864
#&gt; ERR519480     3  0.2165      0.787 0.000 0.064 0.936
#&gt; ERR519487     3  0.3551      0.760 0.000 0.132 0.868
#&gt; ERR519483     2  0.5970      0.463 0.060 0.780 0.160
#&gt; ERR519477     2  0.9998      0.298 0.328 0.344 0.328
#&gt; ERR519499     3  0.1031      0.791 0.000 0.024 0.976
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-2-a').click(function(){
  $('#tab-ATC-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-3'>
<p><a id='tab-ATC-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; ERR519515     1   0.139     0.7710 0.952 0.048 0.000 0.000
#&gt; ERR519516     1   0.326     0.6908 0.844 0.152 0.000 0.004
#&gt; ERR519520     1   0.692     0.5342 0.680 0.160 0.084 0.076
#&gt; ERR519513     2   0.717     0.3354 0.076 0.564 0.328 0.032
#&gt; ERR519481     1   0.455     0.6522 0.732 0.012 0.000 0.256
#&gt; ERR519491     1   0.238     0.7654 0.916 0.068 0.000 0.016
#&gt; ERR519473     4   0.659     0.2831 0.060 0.016 0.336 0.588
#&gt; ERR519518     3   0.516     0.4939 0.040 0.028 0.776 0.156
#&gt; ERR519512     1   0.725     0.4722 0.656 0.128 0.148 0.068
#&gt; ERR519521     1   0.249     0.7599 0.912 0.068 0.000 0.020
#&gt; ERR519488     1   0.455     0.5199 0.732 0.256 0.000 0.012
#&gt; ERR519493     1   0.220     0.7724 0.928 0.048 0.000 0.024
#&gt; ERR519514     1   0.117     0.7811 0.968 0.012 0.000 0.020
#&gt; ERR519479     1   0.397     0.7253 0.804 0.016 0.000 0.180
#&gt; ERR519509     1   0.227     0.7552 0.912 0.084 0.000 0.004
#&gt; ERR519472     4   0.494     0.4295 0.280 0.000 0.020 0.700
#&gt; ERR519510     1   0.409     0.5788 0.764 0.232 0.000 0.004
#&gt; ERR519470     1   0.283     0.7656 0.876 0.004 0.000 0.120
#&gt; ERR519495     1   0.333     0.7552 0.864 0.024 0.000 0.112
#&gt; ERR519522     1   0.182     0.7643 0.936 0.060 0.000 0.004
#&gt; ERR519523     1   0.294     0.7676 0.900 0.052 0.004 0.044
#&gt; ERR519503     4   0.540     0.3787 0.000 0.068 0.212 0.720
#&gt; ERR519471     1   0.737     0.2575 0.516 0.140 0.008 0.336
#&gt; ERR519500     4   0.515     0.1525 0.396 0.008 0.000 0.596
#&gt; ERR519485     2   0.503     0.6259 0.284 0.696 0.004 0.016
#&gt; ERR519476     3   0.999    -0.0149 0.252 0.232 0.268 0.248
#&gt; ERR519502     1   0.680     0.5167 0.652 0.056 0.056 0.236
#&gt; ERR519486     2   0.587     0.6134 0.308 0.644 0.040 0.008
#&gt; ERR519478     1   0.267     0.7735 0.892 0.008 0.000 0.100
#&gt; ERR519497     3   0.883     0.2024 0.172 0.208 0.504 0.116
#&gt; ERR519467     1   0.452     0.6738 0.736 0.012 0.000 0.252
#&gt; ERR519489     4   0.865     0.1583 0.196 0.048 0.352 0.404
#&gt; ERR519494     3   0.548     0.4138 0.016 0.036 0.720 0.228
#&gt; ERR519474     2   0.674     0.5079 0.304 0.576 0.000 0.120
#&gt; ERR519505     4   0.870    -0.0514 0.096 0.364 0.116 0.424
#&gt; ERR519517     3   0.177     0.5894 0.000 0.044 0.944 0.012
#&gt; ERR519484     2   0.566     0.3594 0.436 0.540 0.000 0.024
#&gt; ERR519498     2   0.761     0.4830 0.148 0.576 0.244 0.032
#&gt; ERR519490     3   0.331     0.5217 0.000 0.004 0.840 0.156
#&gt; ERR519507     1   0.412     0.7218 0.796 0.020 0.000 0.184
#&gt; ERR519511     1   0.254     0.7725 0.904 0.012 0.000 0.084
#&gt; ERR519468     3   0.361     0.5714 0.000 0.060 0.860 0.080
#&gt; ERR519482     3   0.256     0.5882 0.000 0.056 0.912 0.032
#&gt; ERR519475     3   0.999    -0.0149 0.252 0.232 0.268 0.248
#&gt; ERR519496     1   0.282     0.7771 0.900 0.036 0.000 0.064
#&gt; ERR519506     4   0.557     0.3950 0.024 0.196 0.044 0.736
#&gt; ERR519469     4   0.597     0.0903 0.008 0.024 0.444 0.524
#&gt; ERR519480     3   0.234     0.5854 0.000 0.020 0.920 0.060
#&gt; ERR519487     3   0.259     0.5771 0.000 0.080 0.904 0.016
#&gt; ERR519483     2   0.519     0.3673 0.028 0.784 0.056 0.132
#&gt; ERR519477     3   0.999    -0.0149 0.252 0.232 0.268 0.248
#&gt; ERR519499     3   0.139     0.5861 0.000 0.012 0.960 0.028
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-3-a').click(function(){
  $('#tab-ATC-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-4'>
<p><a id='tab-ATC-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; ERR519515     1   0.218     0.6438 0.912 0.008 0.000 0.008 0.072
#&gt; ERR519516     1   0.499     0.3015 0.628 0.016 0.000 0.020 0.336
#&gt; ERR519520     1   0.698     0.3991 0.596 0.012 0.092 0.088 0.212
#&gt; ERR519513     5   0.649     0.3368 0.060 0.036 0.304 0.020 0.580
#&gt; ERR519481     1   0.513     0.4623 0.644 0.024 0.000 0.308 0.024
#&gt; ERR519491     1   0.336     0.6138 0.840 0.012 0.000 0.020 0.128
#&gt; ERR519473     4   0.676     0.0349 0.112 0.020 0.348 0.508 0.012
#&gt; ERR519518     3   0.407     0.5814 0.008 0.008 0.760 0.216 0.008
#&gt; ERR519512     1   0.774     0.3441 0.540 0.020 0.152 0.108 0.180
#&gt; ERR519521     1   0.333     0.6569 0.860 0.008 0.004 0.044 0.084
#&gt; ERR519488     1   0.571     0.0644 0.544 0.048 0.004 0.012 0.392
#&gt; ERR519493     1   0.441     0.4864 0.732 0.012 0.000 0.024 0.232
#&gt; ERR519514     1   0.200     0.6649 0.924 0.000 0.000 0.036 0.040
#&gt; ERR519479     1   0.404     0.6446 0.808 0.032 0.000 0.132 0.028
#&gt; ERR519509     1   0.336     0.5839 0.824 0.012 0.000 0.008 0.156
#&gt; ERR519472     4   0.608    -0.1156 0.432 0.052 0.024 0.488 0.004
#&gt; ERR519510     1   0.571    -0.0553 0.500 0.024 0.004 0.028 0.444
#&gt; ERR519470     1   0.263     0.6632 0.900 0.020 0.000 0.056 0.024
#&gt; ERR519495     1   0.400     0.5807 0.748 0.004 0.000 0.232 0.016
#&gt; ERR519522     1   0.325     0.6205 0.848 0.008 0.000 0.024 0.120
#&gt; ERR519523     1   0.378     0.6520 0.832 0.012 0.012 0.116 0.028
#&gt; ERR519503     4   0.661     0.0261 0.040 0.384 0.068 0.500 0.008
#&gt; ERR519471     1   0.853    -0.1044 0.360 0.180 0.008 0.284 0.168
#&gt; ERR519500     1   0.515     0.1262 0.492 0.012 0.012 0.480 0.004
#&gt; ERR519485     5   0.592     0.3648 0.232 0.156 0.004 0.000 0.608
#&gt; ERR519476     4   0.991     0.2399 0.156 0.208 0.236 0.236 0.164
#&gt; ERR519502     1   0.614     0.3431 0.568 0.008 0.068 0.336 0.020
#&gt; ERR519486     5   0.532     0.4944 0.284 0.028 0.036 0.000 0.652
#&gt; ERR519478     1   0.208     0.6686 0.908 0.008 0.000 0.084 0.000
#&gt; ERR519497     3   0.751    -0.1514 0.120 0.036 0.460 0.032 0.352
#&gt; ERR519467     1   0.541     0.5330 0.696 0.076 0.000 0.200 0.028
#&gt; ERR519489     4   0.736     0.1616 0.224 0.016 0.288 0.456 0.016
#&gt; ERR519494     3   0.483     0.4998 0.004 0.012 0.676 0.288 0.020
#&gt; ERR519474     5   0.726    -0.2596 0.204 0.356 0.000 0.032 0.408
#&gt; ERR519505     5   0.883     0.1540 0.076 0.312 0.068 0.184 0.360
#&gt; ERR519517     3   0.184     0.6817 0.000 0.008 0.932 0.008 0.052
#&gt; ERR519484     5   0.649     0.3215 0.372 0.080 0.004 0.032 0.512
#&gt; ERR519498     5   0.669     0.4211 0.116 0.036 0.244 0.012 0.592
#&gt; ERR519490     3   0.492     0.5740 0.000 0.036 0.728 0.200 0.036
#&gt; ERR519507     1   0.414     0.6405 0.808 0.036 0.000 0.120 0.036
#&gt; ERR519511     1   0.339     0.6461 0.836 0.008 0.000 0.132 0.024
#&gt; ERR519468     3   0.516     0.5940 0.000 0.056 0.748 0.080 0.116
#&gt; ERR519482     3   0.269     0.6814 0.000 0.060 0.896 0.028 0.016
#&gt; ERR519475     4   0.991     0.2399 0.156 0.208 0.236 0.236 0.164
#&gt; ERR519496     1   0.285     0.6679 0.888 0.012 0.000 0.052 0.048
#&gt; ERR519506     4   0.620    -0.0291 0.040 0.444 0.016 0.476 0.024
#&gt; ERR519469     3   0.658     0.1346 0.004 0.176 0.420 0.400 0.000
#&gt; ERR519480     3   0.207     0.6897 0.000 0.032 0.928 0.028 0.012
#&gt; ERR519487     3   0.322     0.6519 0.000 0.020 0.856 0.016 0.108
#&gt; ERR519483     2   0.587     0.0000 0.016 0.540 0.024 0.024 0.396
#&gt; ERR519477     4   0.991     0.2399 0.156 0.208 0.236 0.236 0.164
#&gt; ERR519499     3   0.120     0.6826 0.000 0.000 0.956 0.040 0.004
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-4-a').click(function(){
  $('#tab-ATC-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-5'>
<p><a id='tab-ATC-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; ERR519515     1   0.428    0.57988 0.732 0.068 0.000 0.008 0.192 0.000
#&gt; ERR519516     1   0.690    0.05535 0.376 0.352 0.000 0.032 0.228 0.012
#&gt; ERR519520     1   0.400    0.52860 0.828 0.056 0.052 0.016 0.028 0.020
#&gt; ERR519513     2   0.512    0.18406 0.088 0.684 0.200 0.020 0.004 0.004
#&gt; ERR519481     5   0.412    0.57345 0.116 0.024 0.004 0.036 0.800 0.020
#&gt; ERR519491     1   0.623    0.23814 0.456 0.192 0.000 0.012 0.336 0.004
#&gt; ERR519473     5   0.780   -0.11909 0.040 0.056 0.332 0.064 0.428 0.080
#&gt; ERR519518     3   0.519    0.53700 0.000 0.044 0.688 0.036 0.208 0.024
#&gt; ERR519512     1   0.511    0.49256 0.752 0.060 0.100 0.024 0.048 0.016
#&gt; ERR519521     5   0.631    0.01186 0.352 0.168 0.000 0.016 0.456 0.008
#&gt; ERR519488     1   0.386    0.47169 0.800 0.136 0.012 0.020 0.000 0.032
#&gt; ERR519493     1   0.655    0.18076 0.408 0.240 0.000 0.004 0.328 0.020
#&gt; ERR519514     1   0.272    0.62443 0.868 0.012 0.000 0.004 0.104 0.012
#&gt; ERR519479     5   0.557    0.50754 0.128 0.124 0.000 0.020 0.684 0.044
#&gt; ERR519509     1   0.409    0.61752 0.784 0.076 0.000 0.012 0.120 0.008
#&gt; ERR519472     5   0.711    0.45487 0.168 0.040 0.040 0.044 0.580 0.128
#&gt; ERR519510     2   0.640    0.23066 0.172 0.540 0.000 0.016 0.244 0.028
#&gt; ERR519470     1   0.350    0.61166 0.808 0.004 0.000 0.000 0.128 0.060
#&gt; ERR519495     5   0.431    0.35658 0.308 0.032 0.000 0.004 0.656 0.000
#&gt; ERR519522     1   0.224    0.62819 0.904 0.024 0.000 0.004 0.064 0.004
#&gt; ERR519523     1   0.454    0.49572 0.672 0.024 0.008 0.008 0.284 0.004
#&gt; ERR519503     6   0.530    0.45017 0.180 0.004 0.084 0.016 0.024 0.692
#&gt; ERR519471     1   0.564    0.14441 0.600 0.052 0.016 0.028 0.004 0.300
#&gt; ERR519500     5   0.610    0.46784 0.208 0.032 0.024 0.044 0.644 0.048
#&gt; ERR519485     2   0.692   -0.25931 0.136 0.424 0.004 0.368 0.056 0.012
#&gt; ERR519476     2   0.993    0.18136 0.144 0.216 0.144 0.144 0.164 0.188
#&gt; ERR519502     5   0.466    0.56655 0.124 0.028 0.052 0.012 0.768 0.016
#&gt; ERR519486     2   0.659    0.16814 0.224 0.576 0.016 0.120 0.052 0.012
#&gt; ERR519478     1   0.427    0.53137 0.696 0.012 0.000 0.012 0.268 0.012
#&gt; ERR519497     3   0.790    0.00134 0.204 0.324 0.356 0.032 0.016 0.068
#&gt; ERR519467     1   0.546    0.50818 0.692 0.020 0.004 0.028 0.108 0.148
#&gt; ERR519489     5   0.691    0.16548 0.060 0.052 0.284 0.068 0.528 0.008
#&gt; ERR519494     3   0.601    0.44450 0.000 0.056 0.592 0.056 0.272 0.024
#&gt; ERR519474     4   0.689    0.41439 0.124 0.200 0.000 0.556 0.084 0.036
#&gt; ERR519505     6   0.706    0.08962 0.096 0.400 0.036 0.020 0.032 0.416
#&gt; ERR519517     3   0.290    0.63747 0.016 0.112 0.856 0.012 0.000 0.004
#&gt; ERR519484     2   0.651    0.19613 0.112 0.596 0.000 0.080 0.184 0.028
#&gt; ERR519498     2   0.501    0.24079 0.168 0.696 0.112 0.004 0.000 0.020
#&gt; ERR519490     3   0.494    0.56469 0.004 0.036 0.740 0.068 0.136 0.016
#&gt; ERR519507     5   0.571    0.51302 0.112 0.132 0.000 0.032 0.680 0.044
#&gt; ERR519511     5   0.488    0.51559 0.140 0.120 0.000 0.012 0.716 0.012
#&gt; ERR519468     3   0.596    0.38882 0.048 0.136 0.636 0.016 0.000 0.164
#&gt; ERR519482     3   0.212    0.66166 0.004 0.028 0.920 0.036 0.008 0.004
#&gt; ERR519475     2   0.993    0.18136 0.144 0.216 0.144 0.144 0.164 0.188
#&gt; ERR519496     1   0.559    0.34510 0.564 0.072 0.000 0.028 0.332 0.004
#&gt; ERR519506     6   0.309    0.38176 0.012 0.056 0.004 0.020 0.036 0.872
#&gt; ERR519469     6   0.731    0.15341 0.108 0.036 0.344 0.012 0.060 0.440
#&gt; ERR519480     3   0.377    0.64307 0.000 0.088 0.824 0.016 0.048 0.024
#&gt; ERR519487     3   0.389    0.60261 0.028 0.164 0.784 0.016 0.004 0.004
#&gt; ERR519483     4   0.379    0.50167 0.028 0.080 0.016 0.832 0.008 0.036
#&gt; ERR519477     2   0.993    0.18136 0.144 0.216 0.144 0.144 0.164 0.188
#&gt; ERR519499     3   0.135    0.66128 0.008 0.004 0.956 0.008 0.020 0.004
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-5-a').click(function(){
  $('#tab-ATC-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-get-signatures'>
<ul>
<li><a href='#tab-ATC-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-1-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-1"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-2-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-2"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-3-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-3"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-4-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-4"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-5-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-NMF-signature_compare](figure_cola/ATC-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-NMF-collect-classes](figure_cola/ATC-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

## Session info


```r
sessionInfo()
```

```
#> R version 3.6.0 (2019-04-26)
#> Platform: x86_64-pc-linux-gnu (64-bit)
#> Running under: CentOS Linux 7 (Core)
#> 
#> Matrix products: default
#> BLAS:   /usr/lib64/libblas.so.3.4.2
#> LAPACK: /usr/lib64/liblapack.so.3.4.2
#> 
#> locale:
#>  [1] LC_CTYPE=en_GB.UTF-8       LC_NUMERIC=C               LC_TIME=en_GB.UTF-8       
#>  [4] LC_COLLATE=en_GB.UTF-8     LC_MONETARY=en_GB.UTF-8    LC_MESSAGES=en_GB.UTF-8   
#>  [7] LC_PAPER=en_GB.UTF-8       LC_NAME=C                  LC_ADDRESS=C              
#> [10] LC_TELEPHONE=C             LC_MEASUREMENT=en_GB.UTF-8 LC_IDENTIFICATION=C       
#> 
#> attached base packages:
#> [1] grid      stats     graphics  grDevices utils     datasets  methods   base     
#> 
#> other attached packages:
#> [1] genefilter_1.66.0    ComplexHeatmap_2.3.1 markdown_1.1         knitr_1.26          
#> [5] GetoptLong_0.1.7     cola_1.3.2          
#> 
#> loaded via a namespace (and not attached):
#>  [1] circlize_0.4.8       shape_1.4.4          xfun_0.11            slam_0.1-46         
#>  [5] lattice_0.20-38      splines_3.6.0        colorspace_1.4-1     vctrs_0.2.0         
#>  [9] stats4_3.6.0         blob_1.2.0           XML_3.98-1.20        survival_2.44-1.1   
#> [13] rlang_0.4.2          pillar_1.4.2         DBI_1.0.0            BiocGenerics_0.30.0 
#> [17] bit64_0.9-7          RColorBrewer_1.1-2   matrixStats_0.55.0   stringr_1.4.0       
#> [21] GlobalOptions_0.1.1  evaluate_0.14        memoise_1.1.0        Biobase_2.44.0      
#> [25] IRanges_2.18.3       parallel_3.6.0       AnnotationDbi_1.46.1 highr_0.8           
#> [29] Rcpp_1.0.3           xtable_1.8-4         backports_1.1.5      S4Vectors_0.22.1    
#> [33] annotate_1.62.0      skmeans_0.2-11       bit_1.1-14           microbenchmark_1.4-7
#> [37] brew_1.0-6           impute_1.58.0        rjson_0.2.20         png_0.1-7           
#> [41] digest_0.6.23        stringi_1.4.3        polyclip_1.10-0      clue_0.3-57         
#> [45] tools_3.6.0          bitops_1.0-6         magrittr_1.5         eulerr_6.0.0        
#> [49] RCurl_1.95-4.12      RSQLite_2.1.4        tibble_2.1.3         cluster_2.1.0       
#> [53] crayon_1.3.4         pkgconfig_2.0.3      zeallot_0.1.0        Matrix_1.2-17       
#> [57] xml2_1.2.2           httr_1.4.1           R6_2.4.1             mclust_5.4.5        
#> [61] compiler_3.6.0
```


