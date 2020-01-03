<div class="nested0" aria-labelledby="ariaid-title1" topicindex="1" topicid="xju1507161026486" id="xju1507161026486"><h1 class="title topictitle1" id="ariaid-title1">GLM2Predict (ML Engine)</h1><div class="body conbody">
<p class="p">The GLM2Predict function uses the model and (optionally) the regularization table output by the <a href="wdd1577120506488.md#ynr1507159835395">GLM2 (ML Engine)</a> function to perform generalized linear model prediction on new input data.</p></div><div class="topic reference nested1" aria-labelledby="ariaid-title2" topicindex="2" topicid="ymf1507161070573" xml:lang="en-us" lang="en-us" id="ymf1507161070573">
<h2 class="title topictitle2" id="ariaid-title2">GLM2Predict Syntax</h2><div class="body refbody"><div class="section" id="ymf1507161070573__section_N10011_N1000E_N10001">
<h3 class="title sectiontitle">Version 1.2</h3><pre class="pre codeblock" xml:space="preserve"><code>SELECT * FROM GLM2Predict (
  <span>ON { <var class="keyword varname">table</var> | <var class="keyword varname">view</var> | (<var class="keyword varname">query</var>) }</span> AS input PARTITION BY ANY
  <span>ON { <var class="keyword varname">table</var> | <var class="keyword varname">view</var> | (<var class="keyword varname">query</var>) }</span> AS model DIMENSION ORDER BY "category"
  [ <span>ON { <var class="keyword varname">table</var> | <var class="keyword varname">view</var> | (<var class="keyword varname">query</var>) }</span> AS regularization DIMENSION ]
  [ USING 
    [ Lambda (<var class="keyword varname">lambda</var> [,...])) ]
  <code class="ph codeph">[ Accumulate ({ '<var class="keyword varname">accumulate_column</var>' | <var class="keyword varname">accumulate_column_range</var> }[,...]) ]</code>
  ]
) AS <var class="keyword varname">alias</var>;</code></pre></div></div><div class="related-links"><div class="linklistheader"><p></p><b>Related Information</b></div>
<ul class="linklist linklist relinfo"><div class="linklistmember"><a href="ndv1557782188375.md">Column Specification Syntax Elements</a></div></ul></div></div><div class="topic reference nested1" aria-labelledby="ariaid-title3" topicindex="3" topicid="mjn1507161169765" xml:lang="en-us" lang="en-us" id="mjn1507161169765">
<h2 class="title topictitle2" id="ariaid-title3">GLM2Predict Arguments</h2><div class="body refbody"><div class="section" id="mjn1507161169765__section_N10011_N1000E_N10001"><dl class="dl parml"><dt class="dt pt dlterm">Lambda</dt><dd class="dd pd">[Optional if you specify a regularization table, disallowed otherwise] Specify which <var class="keyword varname">lambda</var> values in the regularization table to use to make predictions.
<p class="p">If you omit the regularization table and Lambda argument, the function uses the minLambda value from the model table. (In the model table, minLambda appears in the level column.)</p>
<p class="p">If you specify the regularization table but omit the Lambda argument, the function uses all <var class="keyword varname">lambda</var> values in the regularization table.</p>
<p class="p">If the Lambda argument specifies a <var class="keyword varname">lambda</var> value that is not in the regularization table, the function uses the <var class="keyword varname">lambda</var> value in the regularization table that is closest to the value that you specified.</p></dd><dt class="dt pt dlterm">Accumulate</dt><dd class="dd pd">[Optional] Specify the names of input table columns to copy to the output table.</dd></dl></div></div></div></div>