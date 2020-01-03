<div class="nested0" aria-labelledby="ariaid-title1" topicindex="1" topicid="xcy1506632882935" id="xcy1506632882935"><h1 class="title topictitle1" id="ariaid-title1">IDWT (ML Engine)</h1><div class="body conbody">
<p class="p">The IDWT function is the inverse of <a href="asx1558468105037.md#rpd1506628701823">DWT (ML Engine)</a>; that is, IDWT applies inverse wavelet transforms on multiple sequences simultaneously. IDWT takes as input the output table and meta table output by DWT and outputs the sequences in time domain. (Because the IDWT output is comparable to the DWT input, the inverse transformation is also called the reconstruction.)</p><div class="fig fignone" id="xcy1506632882935__fig_xjp_j3b_mw"><div class="caption"></div><br clear="none"></br><img class="image" id="xcy1506632882935__image_xlx_j3b_mw" src="arm1466005169228.svg" alt="How Machine Learning Engine function IDWT works"></img><br clear="none"></br></div>
<p class="p">This is a typical IDWT use case:</p>
<ol class="ol" id="xcy1506632882935__ol_f2l_xy2_p1b">
<li class="li">Apply DWT to sequences to create their coefficients and corresponding metadata.</li>
<li class="li">Filter the coefficients by methods appropriate for the objects (for example, minimum threshold or top <var class="keyword varname">n</var> coefficients).</li>
<li class="li">Apply IDWT to the filtered coefficients to reconstruct the sequences.</li>
<li class="li">Compare the reconstructed sequences to their original counterparts.</li></ol></div><div class="topic reference nested1" aria-labelledby="ariaid-title2" topicindex="2" topicid="cxy1506632938883" xml:lang="en-us" lang="en-us" id="cxy1506632938883">
<h2 class="title topictitle2" id="ariaid-title2">IDWT Syntax</h2><div class="body refbody"><div class="section" id="cxy1506632938883__section_N1000E_N1000C_N10001">
<h3 class="title sectiontitle">Version ?</h3><pre class="pre codeblock" xml:space="preserve"><code>SELECT * FROM IDWT (
  <span>ON { <var class="keyword varname">table</var> | <var class="keyword varname">view</var> | (<var class="keyword varname">query</var>) }</span> AS InputTable
  <span>ON { <var class="keyword varname">table</var> | <var class="keyword varname">view</var> | (<var class="keyword varname">query</var>) }</span> AS MetaTable
  OUT TABLE OutputTable (<var class="keyword varname">output_table</var>)
  USING
  TargetColumns ({ '<var class="keyword varname">target_column</var>' | <var class="keyword varname">target_column_range</var> }[,... ])
  SortColumn ('<var class="keyword varname">sort_column</var>')
  [ PartitionColumns ({ '<var class="keyword varname">partition_column</var>' | <var class="keyword varname">partition_column_range</var> }[,... ]) ]
) AS <var class="keyword varname">alias</var>;</code></pre></div></div><div class="related-links"><div class="linklistheader"><p></p><b>Related Information</b></div>
<ul class="linklist linklist relinfo"><div class="linklistmember"><a href="ndv1557782188375.md">Column Specification Syntax Elements</a></div></ul></div></div><div class="topic reference nested1" aria-labelledby="ariaid-title3" topicindex="3" topicid="ouc1506633010323" xml:lang="en-us" lang="en-us" id="ouc1506633010323">
<h2 class="title topictitle2" id="ariaid-title3">IDWT Syntax Elements</h2><div class="body refbody"><div class="section" id="ouc1506633010323__section_N10011_N1000E_N10001"><dl class="dl parml"><dt class="dt pt dlterm">OutputTable</dt><dd class="dd pd">Specify the name for the table that the function creates to store the reconstructed result. This table must not exist.</dd><dt class="dt pt dlterm">TargetColumns</dt><dd class="dd pd">Specify the names of the InputTable columns that contain the data to transform. These columns must contain numeric values between -1e308 and 1e308. The function treats NULL as 0.</dd><dt class="dt pt dlterm">SortColumn</dt><dd class="dd pd">Specify the name of the InputTable column that represents the order of coefficients in each sequence (the waveletid column in the DWT output table). The column must contain a sequence of integer values that start from 1 for each sequence. If a value is missing from the sequence, the function treats the corresponding data column as 0.</dd><dt class="dt pt dlterm">PartitionColumns</dt><dd class="dd pd">[Optional] Specify the names of the InputTable partition columns, which identify the sequences. Rows with the same partition column values belong to the same sequence. If you specify multiple partition columns, the function treats the first one as the distribute key of the OutputTable and MetaTable.<div class="note note" id="ouc1506633010323__note_N10047_N10043_N1003C_N10018_N10014_N10010_N10001"><span><b>Note</b></span><div class="notebody">The IDWT input tables are the DWT output tables. If you specify this syntax element for DWT, you must also specify it for IDWT; otherwise, the results might not make sense.</div></div></dd><dd class="dd pd ddexpand">Default behavior: All rows belong to one sequence, and the function creates a distribute key column named dwt_id_<var class="keyword varname">random_name</var> in both the OutputTable and MetaTable. In both tables, every cell of dwt_id_<var class="keyword varname">random_name</var> has the value 1.</dd></dl></div></div></div></div>