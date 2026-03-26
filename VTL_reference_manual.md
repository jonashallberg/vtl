1 
 
 1 
SDMX Technical Working Group 2 
VTL Task Force 3 
 4 
 5 
 6 
 7 
 8 
VTL – version 2.0 9 
(Validation & Transformation Language) 10 
 11 
Part 2 – Reference Manual 12 
 13 
 14 
 15 
 16 
 17 
 18 
 19 
 20 
 21 
 22 
 23 
April 2018 24 
 25 
  26 
2 
 
Foreword  27 
The Task force for the Validation and Transformation Language (VTL), created in 2012-2013 under the initiative 28 
of the SDMX Secretariat, is pleased to present the draft version of VTL 2.0. 29 
The SDMX Secretariat launched the VTL work at the end of 2012, moving on from the consideration that SDMX 30 
already had a package for transformations and expressions in its information model, while a specific 31 
implementation language was missing. To make this framework operational, a standard language for defining 32 
validation and transformation rules (operators, their syntax and semantics) had to be adopted, while 33 
appropriate SDMX formats for storing and exchanging rules, and web services to retrieve them, had to be 34 
designed. The present VTL 2.0 package is only concerned with the first element, i.e., a formal definition of each 35 
operator, together with a general description of VTL, its core assumptions and the information model it is based 36 
on. 37 
The VTL task force was set up early in 2013, composed of members of SDMX, DDI and GSIM communities and the 38 
work started in summer 2013. The intention was to provide a language usable by statisticians to express logical 39 
validation rules and transformations on data, described as either dimensional tables or unit-record data. The 40 
assumption is that this logical formalization of validation and transformation rules could be converted into 41 
specific programming languages for execution (SAS, R, Java, SQL, etc.), and would provide at the same time, a 42 
“neutral” business-level expression of the processing taking place, against which various implementations can be 43 
mapped. Experience with existing examples suggests that this goal would be attainable.  44 
An important point that emerged is that several standards are interested in such a kind of language. However, 45 
each standard operates on its model artefacts and produces artefacts within the same model (property of 46 
closure). To cope with this, VTL has been built upon a very basic information model (VTL IM), taking the 47 
common parts of GSIM, SDMX and DDI, mainly using artefacts from GSIM 1.1, somewhat simplified and with 48 
some additional detail. In this way, existing standards (GSIM, SDMX, DDI, others) would be allowed to adopt VTL 49 
by mapping their information model against the VTL IM. Therefore, although a work-product of SDMX, the VTL 50 
language in itself is independent of SDMX and will be usable with other standards as well. Thanks to the 51 
possibility of being mapped with the basic part of the IM of other standards, the VTL IM also makes it possible to 52 
collect and manage the basic definitions of data represented in different standards. 53 
For the reason described above, the VTL specifications are designed at logical level, independently of any other 54 
standard, including SDMX. The VTL specifications, therefore, are self-standing and can be implemented either on 55 
their own or by other standards (including SDMX). In particular, the work for the SDMX implementation of VTL 56 
is going in parallel with the work for designing this VTL version, and will entail a future update of the SDMX 57 
documentation.  58 
The first public consultation on VTL (version 1.0) was held in 2014. Many comments were incorporated in the 59 
VTL 1.0 version, published in March 2015. Other suggestions for improving the language, received afterwards, 60 
fed the discussion for building the draft version 1.1, which contained many new features, was completed in the 61 
second half of 2016 and provided for public consultation until the beginning of 2017.  62 
The high number and wide impact of comments and suggestions induced a high workload on the VTL TF, which 63 
agreed to proceed in two steps for the publication of the final documentation, taking also into consideration that 64 
some first VTL implementation initiatives had already been launched.  The first step, the current one, is 65 
dedicated to fixing some high-priority features and making them as much stable as possible.  A second step, 66 
scheduled for the next period, is aimed at acknowledging and fixing other features considered of minor impact 67 
and priority, which will be added hopefully without affecting neither the features already published in this 68 
documentation, nor the possible relevant implementations. Moreover, taking into account the number of very 69 
important new features that have been introduced in this version in respect to the VTL 1.0, it was agreed that the 70 
current VTL version should be considered as a major one and thus named VTL 2.0. 71 
The VTL 2.0 package contains the general VTL specifications, independently of the possible implementations of 72 
other standards; in its final release, it will include: 73 
a) Part 1 – the user manual, highlighting the main characteristics of VTL, its core assumptions and the 74 
information model the language is based on; 75 
b) Part 2 – the reference manual, containing the full library of operators ordered by category, including 76 
examples; this version will support more validation and compilation needs compared to VTL 1.0.   77 
c) eBNF notation (extended Backus-Naur Form) which is the technical notation to be used as a test bed for 78 
all the examples.  79 
The present document is the part 2.   80 
3 
 
The latest version of VTL is freely available online at https://sdmx.org/?page_id=5096  81 
 82 
Acknowledgements  83 
The VTL specifications have been prepared thanks to the collective input of experts from Bank of Italy, Bank for 84 
International Settlements (BIS), European Central Bank (ECB), Eurostat, ILO, INEGI-Mexico, ISTAT-Italy, OECD, 85 
Statistics Netherlands, and UNESCO. Other experts from the SDMX Technical Working Group, the SDMX 86 
Statistical Working Group and the DDI initiative were consulted and participated in reviewing the 87 
documentation. 88 
The list of contributors and reviewers includes the following experts: Sami Airo, Foteini Andrikopoulou, David 89 
Barraclough, Luigi Bellomarini, Marc Bouffard, Maurizio Capaccioli, Vincenzo Del Vecchio, Fabio Di Giovanni, Jens 90 
Dossé, Heinrich Ehrmann, Bryan Fitzpatrick, Tjalling Gelsema, Luca Gramaglia, Arofan Gregory, Gyorgy Gyomai, 91 
Edgardo Greising, Dragan Ivanovic, Angelo Linardi, Juan Munoz, Chris Nelson, Stratos Nikoloutsos, Stefano 92 
Pambianco, Marco Pellegrino, Michele Romanelli, Juan Alberto Sanchez, Roberto Sannino, Angel Simon Delgado, 93 
Daniel Suranyi, Olav ten Bosch, Laura Vignola, Fernando Wagener and Nikolaos Zisimos.  94 
Feedback and suggestions for improvement are encouraged and should be sent to the SDMX Technical Working 95 
Group (twg@sdmx.org). 96 
  97 
4 
 
Table of contents 98 
Foreword ........................................................................................................................................................................2 99 
Table of contents .........................................................................................................................................................4 100 
Introduction ..................................................................................................................................................................8 101 
Overwiew of the language and conventions ......................................................................................................9 102 
Introduction ...................................................................................................................................................9 103 
Conventions for writing VTL Transformations ............................................................................................ 10 104 
Typographical conventions ......................................................................................................................... 11 105 
Abbreviations for the names of the artefacts ............................................................................................. 12 106 
Conventions for describing the operators’ syntax ...................................................................................... 12 107 
Description of the data types of operands and result ................................................................................ 14 108 
VTL-ML Operators ....................................................................................................................................... 15 109 
VTL-ML - Evaluation order of the Operators ............................................................................................... 27 110 
Description of VTL Operators ...................................................................................................................... 27 111 
VTL-DL - Rulesets...................................................................................................................................................... 29 112 
define datapoint ruleset ............................................................................................................................. 29 113 
define hierarchical ruleset .......................................................................................................................... 31 114 
VTL-DL – User Defined Operators ...................................................................................................................... 39 115 
define operator ........................................................................................................................................... 39 116 
Data type syntax ......................................................................................................................................... 40 117 
VTL-ML - Typical behaviours of the ML Operators ....................................................................................... 42 118 
Typical behaviour of most ML Operators ................................................................................................... 42 119 
Operators applicable on one Scalar Value or Data Set or Data Set Component ........................................ 42 120 
Operators applicable on two Scalar Values or Data Sets or Data Set Components ................................... 43 121 
Operators applicable on more than two Scalar Values or Data Set Components ...................................... 45 122 
Behaviour of Boolean operators ................................................................................................................. 45 123 
Behaviour of Set operators ......................................................................................................................... 46 124 
Behaviour of Time operators ...................................................................................................................... 46 125 
Operators changing the data type .............................................................................................................. 47 126 
Type Conversion and Formatting Mask ...................................................................................................... 48 127 
The Numbers Formatting Mask .............................................................................................................. 48 128 
The Time Formatting Mask ..................................................................................................................... 48 129 
Attribute propagation ................................................................................................................................. 51 130 
VTL-ML  -  General purpose operators .............................................................................................................. 53 131 
5 
 
Parentheses :   ( ) .................................................................................................................................. 53 132 
Persistent assignment :   <- ...................................................................................................................... 53 133 
Non-persistent assignment :   := .............................................................................................................. 55 134 
Membership :      # ................................................................................................................................... 56 135 
User-defined operator call .......................................................................................................................... 57 136 
Evaluation of an external routine :  eval ........................................................................................... 58 137 
Type conversion :  cast ............................................................................................................................. 59 138 
VTL-ML  -  Join operators ....................................................................................................................................... 64 139 
Join : inner_join,  left_join,  full_join,  cross_join .................................................................................. 64 140 
VTL-ML  -  String operators ................................................................................................................................... 73 141 
String concatenation :   || ....................................................................................................................... 73 142 
Whitespace removal :     trim,  rtrim,  ltrim............................................................................................. 74 143 
Character case conversion :    upper/lower ............................................................................................ 75 144 
Sub-string extraction :     substr ............................................................................................................... 76 145 
String pattern replacement:   replace ......................................................................................................... 78 146 
String pattern location :     instr ............................................................................................................... 79 147 
String length :    length ............................................................................................................................ 81 148 
VTL-ML  -  Numeric operators .............................................................................................................................. 84 149 
Unary plus :   + ........................................................................................................................................ 84 150 
Unary minus:   - ....................................................................................................................................... 85 151 
Addition :   + ............................................................................................................................................ 86 152 
Subtraction :   - ....................................................................................................................................... 88 153 
Multiplication :   * ................................................................................................................................... 89 154 
Division :   / ........................................................................................................................................... 91 155 
Modulo :  mod ...................................................................................................................................... 92 156 
Rounding :  round .................................................................................................................................... 94 157 
Truncation :  trunc ................................................................................................................................. 96 158 
Ceiling :  ceil ............................................................................................................................................. 98 159 
Floor:  floor .......................................................................................................................................... 99 160 
Absolute value :  abs ............................................................................................................................. 100 161 
Exponential :  exp .................................................................................................................................. 101 162 
Natural logarithm :  ln ............................................................................................................................ 102 163 
Power :  power ...................................................................................................................................... 104 164 
Logarithm :  log................................................................................................................................... 105 165 
Square root :  sqrt ................................................................................................................................. 106 166 
6 
 
VTL-ML  -  Comparison operators .................................................................................................................... 108 167 
Equal to :   = .......................................................................................................................................... 108 168 
Not equal to :   <> ............................................................................................................................... 109 169 
Greater than :      >        >= ...................................................................................................................... 110 170 
Less than :      <       <= ........................................................................................................................... 112 171 
Between :   between ............................................................................................................................. 114 172 
Element of:   in  / not_in ..................................................................................................................... 115 173 
match_characters   match_characters .................................................................................................. 117 174 
Isnull:   isnull....................................................................................................................................... 118 175 
Exists in :  exists_in ............................................................................................................................. 120 176 
VTL-ML  -  Boolean operators ............................................................................................................................ 122 177 
Logical conjunction:  and ....................................................................................................................... 122 178 
Logical disjunction :  or .......................................................................................................................... 123 179 
Exclusive disjunction :   xor .................................................................................................................... 125 180 
Logical negation :   not ........................................................................................................................... 127 181 
VTL-ML  -  Time operators .................................................................................................................................. 129 182 
Period indicator :  period_indicator ...................................................................................................... 129 183 
Fill time series : fill_time_series ........................................................................................................... 130 184 
Flow to stock :  flow_to_stock ............................................................................................................ 136 185 
Stock to flow :  stock_to_flow ............................................................................................................. 139 186 
Time shift : timeshift ......................................................................................................................... 142 187 
Time aggregation :  time_agg ................................................................................................................ 145 188 
Actual time :     current_date .................................................................................................................... 147 189 
VTL-ML  -  Set operators ...................................................................................................................................... 149 190 
Union:    union ...................................................................................................................................... 149 191 
Intersection :    intersect .................................................................................................................... 150 192 
Set difference :     setdiff ........................................................................................................................ 152 193 
Simmetric difference :   symdiff............................................................................................................. 153 194 
VTL-ML  -  Hierarchical aggregation ............................................................................................................... 155 195 
Hierarchical roll-up :  hierarchy ......................................................................................................... 155 196 
VTL-ML  -  Aggregate and Analytic operators .............................................................................................. 159 197 
Aggregate invocation ................................................................................................................................ 160 198 
Analytic invocation .................................................................................................................................... 163 199 
Counting the number of data points:  count ......................................................................................... 166 200 
Minimum value :  min ............................................................................................................................ 167 201 
7 
 
Maximum value :  max ........................................................................................................................... 168 202 
Median value :  median ....................................................................................................................... 169 203 
Sum :  sum ......................................................................................................................................... 170 204 
Average value :  avg ............................................................................................................................. 172 205 
Population standard deviation :  stddev_pop ....................................................................................... 173 206 
Sample standard deviation :  stddev_samp .......................................................................................... 174 207 
Population variance :  var_pop .............................................................................................................. 175 208 
Sample variance :  var_samp ................................................................................................................. 176 209 
First value : first_value ....................................................................................................................... 177 210 
Last value : last_value ........................................................................................................................ 178 211 
Lag :  lag ................................................................................................................................................ 180 212 
lead :  lead ............................................................................................................................................. 181 213 
Rank :  rank ......................................................................................................................................... 183 214 
Ratio to report :  ratio_to_report ......................................................................................................... 184 215 
VTL-ML  -  Data validation operators.............................................................................................................. 186 216 
check_datapoint ....................................................................................................................................... 186 217 
check_hierarchy ........................................................................................................................................ 188 218 
check ......................................................................................................................................................... 192 219 
VTL-ML  -  Conditional operators ..................................................................................................................... 195 220 
if-then-else :    if .................................................................................................................................... 195 221 
Nvl :   nvl ................................................................................................................................................ 197 222 
VTL-ML  -  Clause operators ............................................................................................................................... 199 223 
Filtering Data Points :  filter ................................................................................................................... 199 224 
Calculation of a Component :  calc ........................................................................................................ 200 225 
Aggregation :  aggr ................................................................................................................................ 201 226 
Maintaining Components:  keep ........................................................................................................... 204 227 
Removal of Components: drop .............................................................................................................. 205 228 
Change of Component name :  rename ................................................................................................ 206 229 
Pivoting :  pivot ................................................................................................................................... 207 230 
Unpivoting : unpivot ............................................................................................................................ 208 231 
Subspace : sub ....................................................................................................................................... 210 232 
 233 
8 
 
Introduction 234 
This document is the Reference Manual of the Validation and Transformation Language (also known as ‘VTL’) 235 
version 2.0.  236 
The VTL 2.0 library of the Operators is described hereinafter.  237 
VTL 2.0 consists of two parts: the VTL Definition Language (VTL-DL) and the VTL Manipulation Language (VTL-238 
ML). 239 
This manual describes the operators of VTL 2.0 in detail (both VTL-DL and VTL-ML) and is organized as follows.  240 
First, in the following Chapter “Overview of the language and conventions”, the general principles of VTL are 241 
summarized, the main conventions used in this manual are presented and the operators of the VTL-DL and VTL-242 
ML are listed. For the operators of the VTL-ML, a table that summarizes the “Evaluation Order” (i.e., the 243 
precedence rules for the evaluation of the VTL-ML operators) is also given. 244 
The following two Chapters illustrate the operators of VTL-DL, specifically for:  245 
 the definition of rulesets and their rules, which can be invoked with appropriate VTL-ML operators (e.g. 246 
to check the compatibility of Data Point values …); 247 
 the definition of custom operators/functions of the VTL-ML, meant to enrich the capabilities of the VTL-248 
ML standard library of operators. 249 
The illustration of VTL-ML begins with the explanation of the common behaviour of some classes of relevant 250 
VTL-ML operators, towards a good understanding of general language characteristics, which we factor out and 251 
do not repeat for each operator, for the sake of compactness.  252 
The remainder of the document illustrates each single operator of the VTL-ML and is structured in chapters, one 253 
for each category of Operators (e.g., general purpose, string, numeric …). For each Operator, there is a specific 254 
section illustrating the syntax, the semantics and giving some examples.  255 
 256 
9 
 
Overwiew of the language and conventions 257 
Introduction 258 
The Validation and Transformation Language is aimed at defining Transformations of the artefacts of the VTL 259 
Information Model, as more extensively explained in the User Manual.  260 
A Transformation consists of a statement which assigns the outcome of the evaluation of an expression to an 261 
Artefact of the IM. The operands of the expression are IM Artefacts as well. A Transformation is made of the 262 
following components: 263 
● A left-hand side, which specifies the Artefact which the outcome of the expression is assigned to (this is 264 
the result of the Transformation);  265 
● An assignment operator, which specifies also the persistency of the left hand side.  The assignment 266 
operators are two, the first one for the persistent assignment (<-) and the other one for the non-267 
persistent assignment (:=).   268 
● A right-hand side, which is the expression to be evaluated, whose inputs are the operands of the 269 
Transformation.  An expression consists in the invocation of VTL Operators in a certain order.   When an 270 
Operator is invoked, for each input Parameter, an actual argument (operand) is passed to the Operator, 271 
which returns an actual argument for the output Parameter.  In the right hand side (the expression), the 272 
Operators can be nested (the output of an Operator invocation can be input of the invocation of another 273 
Operator).  All the intermediate results in an expression are non-persistent. 274 
Examples of Transformations are: 275 
 276 
DS_np  :=   ( DS_1  -  DS_2 )  *  2   ; 277 
DS_p  <-   if  DS_np >= 0   then  DS_np  else  DS_1   ; 278 
 279 
(DS_1 and DS_2 are input Data Sets, DS_np is a non persistent result, DS_p is a persistent result, the invoked 280 
operators (apart the mentioned assignments) are the subtraction (-) the multiplication (*) the choice 281 
(if…then…else), the greater or equal comparison (>=) and the parentheses that control the order of the 282 
operators’ invocations. 283 
Like in the example above, Transformations can interact one another through their operands and results; in fact 284 
the result of a Transformation can be operand of one or more other Transformations. The interacting 285 
Transformations form a graph that is oriented and must be acyclic to ensure the overall consistency, moreover a 286 
given Artefact cannot be result of more than one Transformation (the consistency rules are better explained in 287 
the User Manual, see VTL Information Model / Generic Model for Transformations / Transformations 288 
consistency). In this regard, VTL Transformations have a strict analogy with the formulas defined in the cells of 289 
the spreadsheets.   290 
A set of more interacting Transformations is usually needed to perform a meaningful and self-consistent task  291 
like for example the validation of one or more Data Sets. The smaller set of Transformations to be executed in the 292 
same run is called Transformation Scheme and can be considered as a VTL program. 293 
Not necessarily Transformations need to be written in sequence like a classical software program, in fact they 294 
are associated to the Artefacts they calculate, like it happens in the spreadsheets (each spreadsheet’s formula is 295 
associated to the cell it calculates). 296 
Nothing prevents, however, from writing the Transformations in sequence, taking into account that not 297 
necessarily the Transformations are performed in the same order as they are written, because the order of 298 
execution depends on their input-output relationships (a Transformation which calculates a result that is 299 
operand of other Transformations must be executed first).  For example, if the two Transformations of the 300 
example above were written in the reverse order: 301 
 302 
(i) DS_p  <-   if  DS_np >= 0   then  DS_np  else  DS_1  ; 303 
(ii) DS_np  :=   ( DS_1  -  DS_2 )  *  2   ; 304 
 305 
10 
 
All the same the Transformation (ii) would be executed first, because it calculates the Data Set DS_np which is 306 
an operand of the Transformation (i). 307 
When Transformations are written in sequence, a semicolon (;) is used to denote the end of a Transformation 308 
and the beginning of the following one.  309 
 310 
 Conventions for writing VTL Transformations 311 
When more Transformations are written in a text, the following conventions apply. 312 
Transformations: 313 
 A Transformation can be written in one or more lines, therefore the end of a line does not denote the end of 314 
a Transformation. 315 
 The end of a Tranformation is denoted by a semicolon (;). 316 
Comments: 317 
Comments can be inserted within  VTL Transformations using the following syntaxes. 318 
 A multi-line comment is embedded between  /*  and  */  and, obviously, can span over several lines: 319 
/*  multi-line 320 
     comment text  */ 321 
 A single-line comment follows the symbol  //  up to the next end of line: 322 
// text of a comment on a single line 323 
 A sequence of spaces, tabs, end-of-line characters or comments is considered as a single space. 324 
 The characters  /* ,  */ ,  // and the whitespaces can be part of a string literal (within double quotes) but in 325 
such a case they are part of the string characters and do not have any special meaning.  326 
 327 
Examples of valid comments: 328 
Example 1: 329 
/* this is a multi-line 330 
 Comment */ 331 
Example 2: 332 
// this is single-line comment 333 
Example 3: 334 
DS_r  <-   /* A is a dataset */  A +  /* B is a dataset */  B ;   335 
(for the VTL this statement is the Transformation     DS_r  <-  A + B ;  ) 336 
Example 4: 337 
DS_r  :=    DS_1    // my comment 338 
  *  DS_2 ; 339 
(for the VTL this statement is the Transformation     DS_r  :=  DS_1 *  DS_2 ;  ) 340 
  341 
11 
 
Typographical conventions 342 
 343 
The Reference Manual (this manual) uses the normal font Cambria for the text and the other following 344 
typographical conventions: 345 
 346 
Convention Description 
Italics Cambria 
        Basic scalar data types (in the text) 
e.g. “…must have one Identifier of type time_period.  If the Data Set….” 
Bold Arial 
        Keywords  (in the description of the syntax and in the text) 
        e.g. Rule  ::={ ruleName  : } { when antecedentCondition  then }  
                              consequentCondition 
                               { errorcode  errorCode  } 
                  { errorlevel  errorLevel  } 
        e.g. “…..The rename operator allows to rename one or more Components…” 
Italics Arial 
Optional Parameter (in the description of the syntax) 
e.g. substr ( op, start, length ) 
Underlined Arial         Sub-expressions 
Normal font Arial 
 The operator’s syntax (excluded  the keywords, the optional Parameters and the 
sub-expressions) 
e.g.  length ( "Hello, World!" ) 
 The examples of invocation of the operators 
e.g.  length ( "Hello, World!" ) 
 Optional and Mandatory Parameters (in the text) 
                 e.g.  “……If comp is a Measure in op, then in the result …..” 
 347 
  348 
12 
 
Abbreviations for the names of the artefacts 349 
The names of the artefacts operated by the VTL-ML come from the VTL IM. In their turn, the names of the VTL IM 350 
artefacts are derived as much as possible from the names of the GSIM IM artefacts, as explained in the User 351 
Manual. 352 
If the complete names are long, the VTL IM suggests also a compact name, which can be used in place of the 353 
complete name in case there is no ambiguity (for example, “Set” instead than “Value Domain Subset”, 354 
“Component” instead than “Data Set Component” and so on); moreover, to make the descriptions more compact, 355 
a number of abbreviations, usually composed of the initials (in capital case) or the first letters of the words of 356 
artefact names, are adopted in this manual: 357 
Complete name   Compact name      Abbreviation 358 
Data Set   Data Set   DS 359 
Data Point   Data Point   DP 360 
Identifier Component  Identifier   Id 361 
Measure Component  Measure   Me 362 
Attribute Component  Attribute   At 363 
Data Set Component  Component   Comp   364 
Value Domain Subset    Subset or Set   Set 365 
Value Domain   Domain    VD 366 
A positive integer suffix (with or without an underscore) can be added in the end to distinguish more than one 367 
instance of the same artefact (e.g., DS_1, DS_2, …, DS_N,    Me1, Me2, …MeN ). The suffix “r” stands for the result of 368 
a Transformation (e.g., DS_r). 369 
Conventions for describing the operators’ syntax 370 
Each VTL operator has an explanatory name, which recalls the operator function (e.g., “Greater than”) and a 371 
syntactical symbol, which is used to invoke the operator (e.g., “>”). The operator symbol may also be alphabetic, 372 
always lowercase (e.g., round). 373 
In the VTL-DL, the operator symbol is the keyword define followed by the name of the object to be defined. The 374 
complete operator symbol is therefore a compound lowercase sentence (e.g. define operator). 375 
In the VTL-ML, the operator symbol does not contain spaces and may be either a sequence of special characters 376 
(like +, -, >=, <= and so on) or a text keyword (e.g., and, or, not). The keyword may be compound with 377 
underscores as separators (e.g., exists_in).  378 
Each operator has a syntax, which is a set of formal rules to invoke the operator correctly. In this document, the 379 
syntax of the operators is formally described by means of a meta-syntax which is not part of the VTL language, 380 
but has only presentation purposes. 381 
The meta-syntax describes the syntax of the operators by means of meta-expressions, which define how the 382 
invocations of the operators must be written. The meta-expressions contain the symbol of the operator (e.g., 383 
“join”), the possible other keywords to denote special parameters (e.g., using), other symbols to be used (e.g., 384 
parentheses, commas), the named formal parameters (e.g., multiplicand and multiplier for the multiplication).   385 
As for the typographic stile, in order to distinguish between the syntax symbols (which are used in the operator 386 
invocations) and meta-syntax symbols (used just for explanatory purposes, and not actually used in invocations), 387 
the syntax symbols are in boldface (i.e., the operator symbol, the special keywords, the possible parenthesis, 388 
commas an so on). The names of the generic operands (e.g., multiplicand, multiplier) are in Roman type, even if 389 
they are part of the syntax.   390 
The meta-expression can be very simple, for example the meta-expression for the addition is: 391 
op1 + op2      392 
This means that the addition has two operands (op1, op2) and is invoked by specifying the name of the first 393 
addendum (op1), then the addition symbol (+) followed by the name of the second addendum (op2).  394 
In this example, all the three parts of the meta-expression are fixed. In other cases, the meta-expression can be 395 
more complex and made of optional, alternative or repeated parts.  396 
In the simple cases, the optional parts are denoted by using the italic face, for example: 397 
13 
 
substr ( op, start, length ) 398 
The expression above implies that in the substr operator the start and length operands are optional. In the 399 
invocation, a non-specified optional operand is substituted by an underscore or, if it is in the end of the 400 
invocation, can be omitted. Hence the following syntaxes are all formally correct: 401 
substr ( op, start, length ) 402 
substr ( op, start ) 403 
substr ( op, _ , length ) 404 
substr ( op ) 405 
In more complex cases, a regular expression style is used to denote the parts (sub-expressions) of the meta-406 
expression that are optional, alternative or repeated. In particular, braces denote a sub-expression; a vertical bar 407 
(or sometimes named “pipe”) within braces denotes possible alternatives; an optional trailing number, following 408 
the braces, specifies the number of possible repetitions.  409 
 non-optional :  non-optional sub-expression (text without braces) 410 
 {optional}  : optional sub-expression (zero or 1 occurrence)  411 
 {non-optional}1 : non-optional sub-expression (just 1 occurrence)  412 
 {one-or-more}+ : sub-expression repeatable from 1 to many occurrences 413 
 {zero-or-more}* : sub-expression repeatable from 0 to many occurrences 414 
 { part1 | part2 | part3 } : optional alternative sub-expressions (zero or 1 occurrence)  415 
 { part1 | part2 | part3 }1  : alternative sub-expressions (just 1 occurrence)  416 
 { part1 | part2 | part3 }+   : alternative sub-expressions, from 1 to many occurrences 417 
 { part1 | part2 | part3 }*  : alternative sub-expressions, from 0 to many occurrences 418 
Moreover, to improve the readability, some sub-expressions (the underlined ones) can be referenced by their 419 
names and separately defined, for example a meta-expression can take the following form:   420 
sub-expr1-text    sub-expr2-name   …    sub-exprN-1-name    sub-exprN-text 421 
sub-expr2-name  ::=  sub-expr2-text 422 
...  possible others ... 423 
sub-exprN-1-name  ::=  sub-exprN-1-text 424 
In this representation of a meta-expression: 425 
 The first line is the text of the meta-expression 426 
 sub-expr1-text, sub-exprN-text    are sub-expressions directly written in the meta-expression 427 
 sub-expr2-name, … sub-exprN-1-name  are identifiers of sub-expressions. 428 
 sub-expr2-text, … sub-exprN-1-text   are subexpression written separately from the meta-expression. 429 
 The symbol  ::=  means “is defined as” and denotes the assignment of a sub-expression-text to a sub-430 
expression-name. 431 
The following example shows  the definition of the syntax of the operators for removing the leading and/or the 432 
trailing whitespaces from a string: 433 
Meta-expression  ::=  { trim | ltrim | rtrim }1 ( op ) 434 
The meta-expression above synthesizes that: 435 
 trim, ltrim, rtrim are the operators’ symbols (reserved keywords); 436 
  (, )  are symbols of the operators syntax (reserved keywords); 437 
 op  is the only operand of the three operators; 438 
 “{  }1”    and  “|”   are symbols of the meta-syntax;  in particular “|” indicates that the three operators are 439 
alternative (a single invocation can contain only one of them) and “{  }1” indicates that a single invocation 440 
contains just one of the shown alternatives; 441 
From this template, it is possible to infer some valid possible invocations of the operators: 442 
ltrim ( DS_2 ) 443 
rtrim ( DS_3 ) 444 
In these invocations, ltrim and rtrim are the symbols of the invoked operator and DS_2 and DS_3 are the names 445 
of the specific Data Sets which are operands respectively of the former and the latter invocation.  446 
 447 
14 
 
Description of the data types of operands and result  448 
This section cointains a brief legenda of the meaning of the symbols used for describing the possible types of 449 
operands and results of the VTL operators. For a complete description of the VTL data types, see the chapter 450 
“VLT Data Types” in the User Manual.  451 
Symbol Meaning Example Example meaning 
parameter  ::  type2 parameter is of the type2 param1 :: string param1 is of type string 
type1 |  type2 alternative types dataset | component  
| scalar 
either datset or component 
or scalar 
type1<type2> scalar type2 restricts type1 measure<string> Measure of string type 
type1 _  (underscore) type1 can appear just once measure<string> _ just one string Measure 
type1 elementName predetermined element of 
type1 measure<string> my_text just one string Measure 
named “my_text” 
type1 _ + type1 can appear one or 
more times measure<string>_+ one or more string 
Measures 
type1 _ * type1 can appear zero, one 
or more times measure<string>_* zero, one or more string 
Measures 
dataset { type_constraint 
} 
Type_constraint restricts 
the dataset type 
dataset { measure < string 
> _+ } 
Dataset having one or 
more string Measures 
t1 * t2  * … * tn Product of the types 
t1 , t2 ,  … , tn string * integer * boolean 
triple of scalar values 
made of a string, an 
integer and a boolean 
value 
t1   ->  t2 Operator  from  
 t1   to  t2 string -> number Operator having input 
string and output number 
ruleset { type_constraint 
} 
Type_constraint restricts 
the ruleset type hierarchical { geo_area } hierarchical ruleset 
defined on geo_area 
set < t > Set of elements of type “t” set < dataset > set of datasets 
 452 
Moreover, the word “name”  in the data type description denotes the fact that the argument of the invocation can 453 
contain only the name of an artefact of such a type but not a sub-expression. For example: 454 
comp ::  name < component < string > > 455 
Means that the argument passed for the input parameter  comp can be only the name of a Component of the 456 
basic scalar type string. The argument passed for comp cannot be a component expression. 457 
The word “name” added as a suffix to the parameter name means the same (for example if the parameter above 458 
is called comp_name).  459 
15 
 
VTL-ML Operators 460 
 461 
Name Symbol Syntax Description Notati
on Input parameters type Result type Behaviour 
Parentheses ( ) ( op ) 
 
Override the 
default 
evaluation 
order of the 
operators 
 
Func. op :: dataset  |  component |   scalar 
dataset    
|component  
| scalar       
Specific 
Persistent 
assignment <- re  <-  op 
Assigns an 
Expression to 
a persistent 
model 
artefact 
Infix op :: dataset dataset    Specific 
Non persistent 
assignment := re  :=  op 
Assigns an 
Expression to 
a non 
persistent 
model 
artefact 
Infix 
op :: dataset 
|   scalar 
 
dataset    Specific 
Membership # ds#comp 
Identifies a 
Component 
within a Data 
Set 
Infix 
ds :: dataset 
 
comp :: name<component> 
 
dataset    Specific 
User defined 
operator call 
 
 operator_name  ( { argument  { , argument }* } ) 
Invokes a 
user defined 
operator 
passing the 
arguments 
Func. 
operatorName ::  name 
 
argument ::  user-defined operator 
parameters data type 
user-defined result data type Specific 
Evaluation of 
an external 
routine 
eval 
eval   (  externalRoutineName ( {argument} {, argument }* ) ,  
language, returns  outputType ) 
Evaluates an 
external 
routine 
Func. 
externalRoutineName :: string 
argument :: any dataType 
language :: string 
outputType :: string 
dataset Specific 
16 
 
Type 
conversion cast cast ( op ,scalarType { , mask } ) 
converts to 
the specified 
data type 
Func. 
op :: dataset{ measure<scalar> _ } 
| component<scalar> 
| scalar 
 
scalarType :: scalar type  
 
mask :: string 
dataset{ measure<scalar> _ } 
| component<scalar> 
| scalar 
 
Changing 
data type 
Join 
inner_joi
n, 
left_join, 
full_join, 
cross_joi
n, 
joinOperator ( ds1 { as alias1 }, … ,dsN { as aliasN } 
{ using usingComp } 
{ filter filterCondition } 
{ apply applyExpr 
| calc calcClause 
| aggr aggrClause { groupingClause } 
} 
{ keep comp {, comp }* 
| drop comp {, comp }*  } 
{ rename compFrom to compTo 
{ , compFrom to compTo }* } 
) 
joinOperator::= { inner_join | left_join| full_join | cross_join }1 
calcClause ::=  { calcRole }  calcComp := calcExpr 
{ , { calcRole }  calcComp := calcExpr }* 
calcRole :: { identifier | measure | attribute | viral attribute} 1 
aggrClause ::=  { aggrRole } aggrComp := aggrExpr 
{ , { aggrRole } aggrComp := aggrExpr }* 
aggrRole ::=  { measure | attribute | viral attribute }1 
groupingClause  ::=  { group by idList 
| group except idList 
| group all conversionExpr }1 
{ having havingCondition } 
Inner join, 
left outer join, 
full outer join, 
cross join, 
Func. 
 
ds1, …, dsN :: dataset 
 
alias1, …, aliasN :: name 
 
usingId :: name < component > 
 
filterCondition :: 
component<boolean> 
 
applyExpr :: dataset 
 
calcComp:: name<component> 
 
calcExpr :: component<scalar> 
 
aggrComp :: name<component > 
 
aggrExpr :: component<scalar> 
 
groupingId :: name < identifier > 
 
conversionExpr :: 
component<scalar> 
 
havingCondition :: 
component<boolean> 
 
comp :: name < component > 
 
compFrom :: component<scalar> 
 
compTo :: component<scalar> 
dataset Specific 
String 
concatenation || op1   ||  op2 Concatenates 
two strings Infix 
op1, op2 :: 
dataset { measure<string> _+}  
| component<string> 
|   string       
dataset { measure<string> _+ } 
|  component<string> 
|   string       
On two 
scalars, DSs 
or DSCs 
17 
 
Whitespace 
removal 
trim 
rtrim 
ltrim 
{trim|ltrim|rtrim}1 ( op ) 
Removes 
trailing 
or/and 
leading 
whitespace 
from a string 
Func. 
op ::  
dataset { measure<string> _+ } 
|   component<string> 
|   string       
dataset { measure<string> _+ } 
|   component<string> 
|   string       
On one 
scalar, DS 
or DSC 
Character case 
conversion 
upper 
lower {upper | lower}1 ( op ) 
Converts the 
character 
case of a 
string in 
upper or 
lower case 
Func. 
op ::  
dataset { measure<string> _+  } 
|   component<string> 
|   string       
dataset { measure<string> _+ } 
|   component<string> 
|   string       
On one 
scalar, DS 
or DSC 
Sub-string 
extraction substr substr ( op, start, length ) 
Extracts the 
substring that 
starts in a 
specified 
position and 
has a 
specified 
lengtt 
Func. 
op ::  
dataset { measure<string> _+  } 
|   component<string> 
|   string     
 
start ::  
component < integer[>=1]> 
| integer[>= 1]  
 
length ::  
component < integer[>= 0] > 
| integer[>=0]  
     
dataset { measure<string> _+ } 
|   component<string> 
|   string       
On one DS 
 
or 
 
on more 
than two 
scalars or 
DSC 
String pattern 
replacement replace replace (op ,pattern1, pattern2 ) 
Replaces a 
specified 
string-pattern 
with another 
one 
Func. 
op ::  
dataset { measure<string> _+  } 
|   component<string> 
|   string     
 
pattern1, pattern2 ::  
component<string> 
| string 
 
dataset { measure<string> _+ } 
|   component<string> 
|   string       
On one DS 
 
or 
 
on more 
than two 
scalars or 
DSC 
18 
 
String pattern 
location instr instr( op, pattern, start, occurrence ) 
Returns the 
location of a 
specified 
string-pattern 
Func. 
op ::  
dataset { measure<string> _+  } 
|   component<string> 
|   string     
 
pattern :: component<string> 
|  string 
 
start:: component< integer[ >= 1]>  
|  integer[>= 1]         
 
occurrence ::  
component < integer[>= 1] >  
|  integer[>= 1]        
dataset  
{measure<integer[>=0]> 
int_var } 
|  component <integer[>= 0]> 
|  integer[>= 0]       
 
Changing 
data type 
String length length length ( op ) 
Returns the 
length of a 
string 
Func. 
op ::  
dataset { measure<string> _  } 
|   component<string> 
|   string     
 
dataset  
{measure<integer[>=0]> 
int_var } 
|  component <integer[>= 0]> 
|  integer[>= 0]       
 
Changing 
data type 
Unary plus + + op 
Replicates the 
operand with 
the sign 
unaltered 
Infix 
op :: 
dataset  { measure<number>   _+  } 
|   component<number> 
|   number     
dataset   
{ measure<number>   _+  } 
|   component<number> 
|   number     
On one 
scalar, DS 
or DSC 
Unary minus - - op 
Replicates the 
operand with 
the sign 
changed 
Infix 
op :: 
dataset  { measure<number>   _+  } 
|   component<number> 
|   number     
 dataset  
{ measure<number>   _+  } 
|   component<number> 
|   number     
On one 
scalar, DS 
or DSC 
Addition + op1 + op2 Sums two 
numbers Infix 
op1, op2:: 
dataset  { measure<number>   _+  } 
|   component<number> 
|   number     
dataset  
{ measure<number>   _+  } 
|   component<number> 
|   number     
On two 
scalars, DSs 
or DSCs 
Subtraction - op1 - op2 Subtracts two 
numbers Infix 
op1, op2:: 
dataset  { measure<number>   _+  } 
|   component<number> 
|   number     
dataset  
{ measure<number>   _+  } 
|   component<number> 
|   number     
On two 
scalars, DSs 
or DSCs 
Multiplication * op1  *  op2 Multiplies  
two numbers Infix 
op1, op2:: 
dataset  { measure<number>   _+  } 
|   component<number> 
|   number     
dataset  
{ measure<number>   _+  } 
|   component<number> 
|   number     
On two 
scalars, DSs 
or DSCs 
Division / op1 / op2 Divides two 
numbers Infix 
op1, op2:: 
dataset  { measure<number>   _+  } 
|   component<number> 
|   number     
dataset  
{ measure<number>   _+  } 
|   component<number> 
|   number     
On two 
scalars, DSs 
or DSCs 
19 
 
Modulo mod mod ( op1, op2) 
Calculates the 
remainder of 
a number 
divided by a 
certain 
divisor 
Func. 
op1, op2:: 
dataset  { measure<number>   _+  } 
|   component<number> 
|   number     
dataset  
{ measure<number>   _+  } 
|   component<number> 
|   number     
On two 
scalar, DS 
or DSC 
Rounding round round ( op, numDigit ) 
Rounds a 
number to a 
certain digit 
Func. 
op :: 
dataset  { measure<number>   _+  } 
| component<number> 
| number     
 
numDigit::   
component < integer > | integer 
dataset  
{ measure<number>   _+  } 
|   component<number> 
|   number     
On one DS 
 
or 
 
on two 
scalars or 
DSC 
Truncation trunc trunc ( op, numDigit ) 
Truncates a 
number to a 
certain digit 
Func. 
op :: 
dataset  { measure<number>   _+  } 
|   component<number> 
|   number   
   
numDigit ::   
component < integer > |  integer 
dataset  
{ measure<number>   _+  } 
|   component<number> 
|   number     
On one DS 
 
or 
 
on two 
scalars or 
DSC 
Ceiling ceil ceil ( op ) 
Returns the 
smallest 
integer which 
is greater or 
equal than a 
number 
Func. 
op :: 
dataset  { measure<number>   _+  } 
|   component<number> 
|   number     
dataset   
{ measure<integer>   _+  } 
|   component< integer > 
|   integer 
On one 
scalar, DS 
or DSC 
Floor floor floor ( op ) 
Returns the 
greater 
integer which 
is smaller or 
equal than a 
number 
Func. 
op :: 
dataset  { measure<number>   _+  } 
|   component<number> 
|   number     
dataset  
{ measure<integer>   _+  } 
|   component< integer > 
|   integer 
On one 
scalar, DS 
or DSC 
Absolute value abs abs ( op ) 
Calculates the 
absolute 
value of a 
number 
Func. 
op :: 
dataset { measure<number>   _+  } 
|   component<number> 
|   number 
dataset    
{ measure<number[>=0]> _+ } 
|   component<number[>=0]> 
|   number[>= 0]  
On one 
scalar, DS 
or DSC 
Exponential exp exp ( op ) 
Raises e (base 
of the natural 
logarithm) to 
a number 
Func. 
op:: 
dataset  { measure<number>   _+  } 
|   component<number> 
|   number 
dataset    
{ measure<number[>0]>  _+  } 
|   component<number[>0]> 
|   number[> 0] 
On one 
scalar, DS 
or DSC 
20 
 
Natural 
logarithm ln ln ( op ) 
Calculates the 
natural 
logarithm of a 
number 
Func. 
op :: 
dataset 
{measure<number[>0]> _+ }  
|   component<number[>0]> 
|   number[>0] 
dataset    
{ measure<number> _+  } 
|   component<number> 
|   number 
On one 
scalar, DS 
or DSC 
Power power power (  base, exponent) 
Raises a 
number to a 
certain 
exponent 
Func. 
base :: 
dataset   { measure<number> _+  } 
|   component<number> 
|   number 
 
exponent :: 
component<number> |  number 
dataset    
{ measure<number> _+  } 
|   component<number> 
|   number 
On one DS 
 
or 
 
on two 
scalars or 
DSC 
Logarithm log log ( op, num ) 
Calculates the 
logarithm of a 
number to a 
certain base 
Func. 
op :: dataset  
 { measure<number[>1]> _+  } 
|   component<number[>1]> 
|   number[>1] 
 
num:: component<integer[>0]> 
|  integer[>0]  
dataset  
 { measure<number> _+  } 
|   component<number> 
|   number 
 
On one DS 
 
or 
 
on two 
scalars or 
DSC 
Square root sqrt sqrt ( op ) 
Calculates the 
square root of 
a number 
Func. 
op :: dataset   
 { measure<number[>=0> _+  } 
|   component<number[>= 0]> 
|   number[>= 0] 
dataset    
{ measure<number[>=0]> _+ } 
|   component<number[>= 0]> 
|   number[>= 0] 
On one 
scalar, DS 
or DSC 
Equal to = left  =  rigth 
Verifies if two 
values are 
equal 
Infix 
left,right ::      
dataset   {measure<scalar> _ } 
|  component<scalar> 
|  scalar     
dataset    
{measure<boolean>  bool_var} 
|   component<boolean> 
|   boolean    
Changing 
data type 
Not equal to <> left  <>  rigth 
Verifies if two 
values are not 
equal 
Infix 
left, right :: 
dataset   {measure<scalar> _ } 
|  component<scalar> 
|  scalar     
dataset   
{measure<boolean>  bool_var} 
|   component<boolean> 
|   boolean    
Changing 
data type 
Greater than 
> 
left {  >  |  >= }1 right 
Verifies if a 
first value is 
greater  ( or 
equal ) than a 
second value 
Infix 
left, right :: 
dataset   {measure<scalar> _  } 
|  component<scalar> 
|  scalar     
dataset  
{measure<boolean>  bool_var} 
|   component<boolean> 
|   boolean    
Changing 
data type >= 
Less than 
< 
 left   {  <  |  <=  }1   right 
Verifies if a 
first value is 
less (or 
equal)  than a 
second value 
Infix 
left, right :: 
 dataset   {measure<scalar> _ } 
|  component<scalar> 
|  scalar     
dataset  
{measure<boolean>  bool_var} 
|   component<boolean> 
|   boolean    
Changing 
data type 
<= 
21 
 
Between between between( op, from, to ) 
Verify if a 
value belongs 
to a range of 
values 
Func. 
op ::  
dataset   {measure<scalar> _} 
|  component<scalar> 
|  scalar 
from ::scalar | component<scalar> 
to :: scalar | component<scalar> 
 
dataset   
{measure<boolean>  bool_var} 
|   component<boolean> 
|   boolean    
Changing 
data type 
Element of 
in 
 
op in collection 
collection ::= set  |   valueDomainName 
Verifies if a 
value belongs 
to a set of 
values 
Infix op :: 
dataset   {measure<scalar> _ } 
|  component<scalar> 
|  scalar     
 
collection :: set<scalar>   
|  name<value_domain> 
dataset  
{measure<boolean>  bool_var} 
|   component<boolean> 
|   boolean    
Changing 
data type 
not_in 
op not_in collection 
collection ::= set  |   valueDomainName 
Verifies if a 
value does 
not belong to 
a set of values 
Infix 
Match_charact
ers 
match_c
haracter
s 
match_characters (op, pattern) 
 
Verifies if a 
value 
respects or 
not a pattern 
Func. 
op:: 
dataset   {measure<string> _} 
|  component<string> 
|  string 
 
pattern  ::  
string | component<string> 
dataset  
{measure<boolean>  bool_var} 
|   component<boolean> 
|   boolean    
Changing 
data type 
Isnull isnull isnull ( op ) 
Verifies if a  
values is 
NULL 
Func. 
op :: 
dataset   {measure<scalar> _} 
|  component<scalar> 
|  scalar     
dataset   
{measure<boolean>  bool_var} 
|   component<boolean> 
|   boolean    
Changing 
data type 
Exists in exists_in 
exists_in ( op1, op2, retain) 
retain := { true | false | all } 
 
As for the 
common 
identifiers of 
op1 and op2, 
verifies if the 
combinations 
of values of 
op1 exist in 
op2. 
Func. op1, op2 :: dataset    dataset  
{measure<boolean>  bool_var} 
Changing 
data type 
Logical 
conjunction and op1 and op2 Calculates the 
logical AND  
op1,op2 ::     
dataset   {measure<boolean> _ } 
|  component<boolean> 
|  boolean     
dataset   
 {  measure<boolean>  _} 
|   component<boolean> 
|   boolean    
Boolean 
Logical 
disjunction or op1 or op2 Calculates the 
logical OR  
op1,op2 ::      
dataset   {measure<boolean> _ } 
|  component<boolean> 
|  boolean     
dataset   
{  measure<boolean>  _} 
|   component<boolean> 
|   boolean    
Boolean 
22 
 
Exclusive 
disjunction xor op1 xor op2 Calculates the 
logical XOR  
op1,op2 ::      
dataset   {measure<boolean> _ } 
|  component<boolean> 
|  boolean     
dataset    
{  measure<boolean>  _} 
|   component<boolean> 
|   boolean    
Boolean 
Logical 
negation not not op Calculates the 
logical NOT  
op :: 
dataset   {measure<boolean> _  } 
|  component<boolean> 
|  boolean     
dataset    
{  measure<boolean>  _  } 
|   component<boolean> 
      |   boolean    
Boolean 
Period 
indicator 
period_i
ndicator period_indicator  ( {op} ) 
extracts the 
period 
indicator 
from a 
time_period 
value 
Func. 
op :: 
dataset 
{ identifier <time_period> _  , 
identifier _* } 
| component<time_period> 
| time_period 
dataset { measure<duration> 
duration_var  } 
| component <duration> 
| duration 
Specific 
Fill time series fill_time_
series 
fill_time_series  ( op { , limitsMethod } ) 
limitsMethod ::= single | all 
Replaces each 
missing data 
point in the 
input Data Set 
Func. 
op ::  
dataset  
{ identifier <time> _ , identifier _* } 
dataset  
{ identifier <time> _  , 
identifier _* } 
Specific 
Flow to stock flow_to_s
tock flow_to_stock  ( op ) 
Transforms 
from a flow 
interpretatio
n of a Data 
Set to stock 
Func. 
op :: 
dataset { identifier <time> _ , 
identifier _* ,  
measure<number>   _+  }   
dataset  
{ identifier < time > _ , 
identifier _* ,  
measure<number>   _+  }   
Specific 
Stock to flow stock_to_
flow stock_to_flow  ( op ) 
Transforms 
from stock to  
flow 
interpretatio
n of a Data 
Set  
Func. 
op :: 
dataset  
{ identifier <time> _ , identifier _* ,  
measure<number>   _+  } 
dataset  
{ identifier < time > _ ,  
identifier _* ,  
measure<number>   _+  } 
Specific 
Time shift timeshift timeshift  ( op ,  shiftNumber  ) 
Shifts the 
time 
component of 
a specified 
range of time 
Func. 
op :: 
dataset  
{ identifier <time> _ , identifier _* } 
 
shiftNumber :: integer 
 
dataset  
{ identifier < time > _ , 
identifier _* } 
 
Specific 
Time 
aggregation time_agg time_agg ( periodIndTo { , periodIndFrom } { ,op  }{ , first | last }) 
converts the 
time values 
from higher 
to lower 
frequency 
values 
Func. 
op ::   
dataset  
{ identifier <time> _ , identifier _* } 
|  component<time>  
|  time   
 
periodIndFrom ::  duration 
 
periodIndTo ::  duration 
dataset  
{ identifier < time > _  , 
identifier _* } 
|  component<time>  
|  time   
Specific 
23 
 
Actual time current_
date current_date ( ) returns the 
current date Func.  date Specific 
Union union 
union ( dsList ) 
 dsList ::= ds { , ds }* 
Computes the 
union of N 
datasets 
Func. ds  :: dataset dataset    Set 
Intersection intersect 
intersect ( dsList ) 
 dsList ::= ds { , ds }* 
Computes the 
intersection 
of N datasets 
Func. ds  :: dataset dataset    Set 
Set difference setdiff setdiff ( ds1, ds2 ) 
Computes the 
differences of 
two datasets 
Func. ds1, ds2 ::  dataset dataset    Set 
Simmetric 
difference symdiff symdiff ( ds1, ds2 ) 
Computes the 
symmetric 
difference of 
two datasets 
Func. ds1, ds2  :: dataset dataset    Set 
Hierarchical 
roll-up 
hierarch
y 
hierarchy ( op , hr { condition  condComp { , condComp }* }  
{ rule ruleComp } { mode } { input } { output } ) 
condComp ::= component { , component }* 
mode ::= non_null | non_zero | partial_null | partial_zero | 
always_null | always_zero 
input ::=  dataset | rule | rule_priority  
output ::=  computed | all 
Aggregates 
data using a 
hierarchical 
ruleset 
Func. 
op ::dataset{measure<number> _ }  
hr ::name <  hierarchical >  
condComp :: name < component > 
ruleComp :: name < identifier > 
dataset{measure<number> _ }     Specific 
Aggregate 
invocation  
in a Data Set expression: 
 
aggregateOperator  
( firstOperand  { , additionalOperand }*   { groupingClause }  ) 
  
in a Component  expression within an aggr clause 
 
aggregateOperator  
( firstOperand { , additionalOperand }* )  { groupingClause }  
aggregateOperator ::=   avg | count | max | median | min | 
stddev_pop| stddev_samp | sum | 
var_pop | var_samp  
groupingClause ::=  
 { group by groupingId {, groupingId}*  
|   group except groupingId {, groupingId}*  
|   group all conversionExpr }1    
 { having havingCondition } 
    
Set of 
statistical 
functions 
used to 
aggregate 
data 
Func. 
firstOperand ::  
dataset | component    
 
additionalOperand :: type of the 
(possible) additional parameter of 
the aggregate Operator   
 
groupingId ::name < identifier > 
 
conversionExpr :: identifier 
 
havingCondition :: 
 component<boolean> 
dataset | component Specific 
24 
 
Analytic 
invocation  
analyticOperator 
 ( firstOperand { , additionalOperand }*  over ( analyticClause ) ) 
 
analyticOperator  ::=  avg | count | max | median | min | 
stddev_pop| stddev_samp | sum | var_pop 
| var_samp | first_value | lag | last_value | 
lead | rank | ratio_to_report 
 
analyticClause ::=  
{ partitionClause } { orderClause } { windowClause } 
 
partitionClause ::=  partition by identifier { ,  identifier }* 
 
orderClause  ::=  order by component { asc | desc }  
{ , component { asc | desc } }* 
 
windowClause ::=  
{ data points | range }1  between limitClause and limitClause 
 
limitClause ::=  
{ num preceding | num following | current data point  
| unbounded preceding |   unbounded following }1 
Set of 
statistical 
functions 
used to 
aggregate 
data 
Func. 
firstOperand ::  
dataset  |  component 
 
additionalOperand :: type of the 
(possible) additional parameter of 
the invoked operator   
 
identifier :: name<identifier> 
 
component :: name<component> 
 
num :: integer 
dataset | component Specific 
Check 
datapoint 
check_da
tapoint 
check_datapoint 
 ( op , dpr { components listComp } { output output } ) 
listComp ::= comp { , comp }* 
output ::=  invalid | all | all_measures 
Applies one 
datapoint 
ruleset  on a 
Data Set 
Func. 
op ::dataset 
dpr ::name < datapoint > 
comp :: name < component > 
dataset Specific 
Check 
hierarchy 
check_hi
erarchy 
check_hierarchy ( 
op , hr { condition  condComp { , condComp }* }  
{ rule ruleComp }  
{ mode } { input } { output } ) 
mode ::=  non_null | non_zero | partial_null | partial_zero | 
always_null | always_zero 
input ::=  dataset | dataset_priority 
output ::=  invalid | all | all_measures 
 
Applies a 
hierarchical 
ruleset to a 
Data Set 
Func. 
op ::dataset  
 
hr ::name < hierarchical > 
 
condComp :: name< component > 
 
ruleComp :: name< identifier > 
 
dataset Specific 
Check check 
check ( op { errorcode errorcode } { errorlevel errorlevel }  
{ imbalance imbalance } { output } ) 
output ::=  invalid | all 
Checks if an 
expression 
verifies a 
condition 
Func. 
op :: dataset 
 
errorcode :: errorcode_vd 
 
errorlevel :: errorlevel_vd 
 
imbalance :: number 
 
 
 
dataset 
 
Specific 
25 
 
If then else if ….then 
else…. if condition  then thenOperand else  elseOperand 
Makes 
alternative 
calculations 
according to a 
condition 
Func. 
condition ::  
dataset { measure <boolean> _ }  
|  component<boolean>  
|  boolean 
 
thenOperand :: 
dataset |  component  |  scalar 
 
elseOperand ::  
dataset |  component |  scalar 
dataset    
|   component 
|   scalar 
Specific 
Nvl nvl nvl ( op1, op2 ) 
Replaces the 
null value 
with a value. 
Func. 
op1,  op2::  
dataset    
|   component 
|   scalar 
dataset   
|   component 
|   scalar 
Specific 
Filtering Data 
Points filter op [ filter condition ] 
Filter data 
using a 
Boolean 
condition 
Clause 
op :: dataset  
 
filterCondition :: 
component<boolean> 
dataset Specific 
Calculation of 
a Component calc op [ calc { calcRole } calcComp := calcExpr { , { calcRole } 
calcComp := calcExpr }* ] 
Calculates the 
values of a 
Structure 
Component 
Clause 
op :: dataset 
 
calcComp ::name < component > 
 
calcExpr :: component<scalar> 
dataset Specific 
Aggregation aggr 
op [ aggr aggrClause { groupingClause } ]  
 
aggrClause ::= { aggrRole } aggrComp := aggrExpr  
                             { , { aggrRrole } aggrComp:= aggrExpr }*  
 
groupingClause ::= { group by   groupingId {, gropuingId }*  
| group except groupingId {, groupingId }*  
| group all conversionExpr }1 
  { having havingCondition }   
 
aggrRole::=  measure  |  attribute  |  viral attribute 
Aggregates 
using an 
aggregate 
operator 
Clause 
op :: dataset 
 
aggrComp :: name < component > 
 
aggrExpr :: component<scalar> 
 
groupingId ::name <identifier > 
 
  conversionExpr :: 
identifier<scalar>  
 
havingCondition :: 
component<boolean> 
dataset Specific 
Maintaining 
Components keep op [ keep comp {, comp }* ] Keep list of 
components Clause 
op ::dataset 
 
comp :: name < component > 
dataset Specific 
Removal of 
Components drop op [drop  comp { , comp }* ] Drop list of 
components Clause 
op :: dataset  
 
comp :: name < component > 
dataset Specific 
26 
 
 462 
 463 
Change of 
Component 
name 
rename op [ rename comp_from to comp_to { ,comp_from to comp_to }*  ] Rename 
components Clause 
op :: dataset   
 
comp_from :: name<component> 
 
comp_to :: name<component> 
dataset Specific 
Pivoting pivot op [ pivot identifier , measure ] 
Transform 
identifier 
values to 
measures 
Clause 
op :: dataset 
 
identifier ::name <identifier> 
 
measure ::name <measure> 
dataset Specific 
Unpivoting unpivot op [ unpivot  identifier , measure ] 
Transform  
measures to 
identifier 
values 
Clause 
op :: dataset  
 
identifier :: name<identifier> 
 
measure ::  name<measure> 
 
 
 
 
dataset 
 
Specific 
Subspace sub op [ sub identifier = value { , identifier = value }* ] 
Remove the 
specified 
identifiers by 
fixing a value 
for them 
Clause 
op :: dataset 
 
identifier :: name<identifier> 
 
value :: scalar 
dataset Specific 
27 
 
VTL-ML - Evaluation order of the Operators 464 
Within a single expression of the manipulation language, the operators are applied in sequence, according to the 465 
precedence order. Operators with the same precedence level are applied according to the default associativity 466 
rule. Precedence and associativity orders are reported in the following table. 467 
 468 
Evaluation 
order Operator Description Default 
associativity rule 
I ( ) Parentheses. To alter the default 
order. None 
II VTL operators with 
functional syntax 
VTL operators with functional 
syntax Left-to-right 
III Clause 
Membership 
Clause 
Membership Left-to-right 
IV 
unary plus 
unary minus 
not 
Unary minus 
Unary plus 
Logical negation 
None 
V * 
/ 
Multiplication 
Division Left-to-right 
VI 
+ - 
|| 
Addition 
Subtraction 
String concatenation 
Left-to-right 
VII 
> >= 
< <= 
= 
<> 
in 
not_in 
Greater than 
Less than 
Equal-to 
Not-equal-to 
In a value list 
Not in a value list 
Left-to-right 
VIII and Logical AND Left-to-right 
IX or 
xor 
Logical OR 
Logical XOR Left-to-right 
X if-then-else Conditional (if-then-else) None 
 469 
Description of VTL Operators 470 
 471 
The structure used for the description of the VTL-DL Operators is made of the following parts: 472 
 Operator name, which is also used to invoke the operator  473 
 Semantics:  a brief description of the purpose of the operator  474 
 Syntax:  the syntax of the Operator (this part follows the conventions described in the previous section  475 
“Conventions for describing the operators’ syntax”) 476 
 Syntax description:  detailed explanation of the meaning of the various parts of the syntax  477 
 Parameters: list of the input parameters and their types  478 
28 
 
 Constraints: additional constraints that are not specified with the meta-syntax and need a textual 479 
explanation 480 
 Semantic specifications: detailed description of the semantics of the opoerator  481 
 Examples: examples of invocation of the operator 482 
 483 
The structure used for the description of the VTL-ML Operators is made of the following parts: 484 
 Operator name, followed by the operator symbol (keyword) which is used to invoke the operator  485 
 Syntax:  the syntax of the Operator (this part follows the conventions described in the previous section  486 
“Conventions for describing the operators’ syntax”) 487 
 Input parameters: list of all input parameters and the subexpressions with their meaning and the 488 
indication if they are mandatory or optional  489 
 Examples of valid syntaxes: examples of syntactically valid invocations of the Operator  490 
 Semantics for scalar operations: the behaviour of the Operator on scalar operands, which is the basic 491 
behaviour of the Operator  492 
 Input parameters type: the formal description of the type of the input parameters (this part follows the 493 
conventions described in the previous section “Description of the data types of operands and results”)  494 
 Result type: the formal description of the type of the result (this part follows the conventions described in 495 
the previous section “Description of the data types of operands and results”) 496 
 Additional constraints: additional constraints that are not specified with the meta-syntax and need a 497 
textual explanation, including both possible semantic constraints under which the operation is possible or 498 
impossible, and syntactical constraint for the invocation of the Operator  499 
 Behaviour: description of the behaviour of the Operator for non-scalar operations (for example operations 500 
at Data Set or at Component level).  When the Operator belongs to a class of Operators having a common 501 
behaviour, the common behavior is described once for all in a section of the chapter “Typical behaviours of 502 
the ML Operators” and therefore this part describes only the specific aspect of the behaviour and contains a 503 
reference to the section where the common part of the behaviour is described.  504 
 Examples: a series of examples of invocation and application of the operator in case of operations at Data 505 
Sets or at Component level. 506 
 507 
29 
 
VTL-DL - Rulesets  508 
define datapoint ruleset  509 
Semantics 510 
The Data Point Ruleset contains Rules to be applied to each individual Data Point of a Data Set for validation 511 
purposes.  These rulesets are also called “horizontal” taking into account the tabular representation of a Data Set 512 
(considered as a mathematical function), in which each (vertical) column represents a variable and each 513 
(horizontal) row represents a Data Point: these rulesets are applied on individual Data Points (rows), i.e., 514 
horizontally on the tabular representation.   515 
 516 
Syntax 517 
 518 
define datapoint ruleset  rulesetName  ( dpRulesetSignature ) is 519 
dpRule   520 
{ ;  dpRule }* 521 
end datapoint ruleset  522 
 523 
dpRulesetSignature ::=  valuedomain listValueDomains | variable listVariables 524 
listValueDomains ::=  valueDomain { as vdAlias } { , valueDomain { as vdAlias } }* 525 
listVariables  ::=  variable { as varAlias } { , variable { as varAlias } }* 526 
dpRule  ::= { ruleName : } { when antecedentCondition then } consequentCondition 527 
{ errorcode  errorCode  } 528 
{ errorlevel  errorLevel  } 529 
 530 
Syntax description 531 
rulesetName  the name of the Data Point Ruleset to be defined.  532 
dpRulesetSignature  the Cartesian space of the Ruleset (signature of the Ruleset), which specifies either the 533 
Value Domains or the Represented Variables (see the information model) on which the 534 
Ruleset is defined.  If valuedomain is specified then the Ruleset is applicable to the Data 535 
Sets having Components that take values on the specified Value Domains. If variable is 536 
specified then the Ruleset is applicable to Data Sets having the specified Variables as 537 
Components. 538 
valueDomain  a Value Domain on which the Ruleset is defined.  539 
vdAlias  an (optional) alias assigned to a Value Domain and valid only within the Ruleset, this can 540 
be used  for the sake of compactness in writing the Rules. If an alias is not specified then 541 
the name of the Value Domain (parameter valueDomain) is used in the body of the rules. 542 
variable a Represented Variable on which the Ruleset is defined. 543 
varAlias  an (optional) alias assigned to a Variable and valid only within the Ruleset, this can be 544 
used  for the sake of compactness in writing the Rules. If an alias is not specified then the 545 
name of the Variable  (parameter valueDomain) is used in the body of the Rules. 546 
dpRule  a Data Point Rule, as defined in the following parameters. 547 
ruleName  the name assigned to the specific Rule within the Ruleset. If the Ruleset is used for 548 
validation then the ruleName identifies the validation results of the various Rules of the 549 
Ruleset. The ruleName is optional and, if not specified, is assumed to be the progressive 550 
order number of the Rule in the Ruleset. However please note that, if ruleName is 551 
omitted, then the Rule names can change in case the Ruleset is modified, e.g., if new Rules 552 
are added or existing Rules are deleted, and therefore the users that interpret the 553 
validation results must be aware of these changes. 554 
antecedentCondition a boolean expression to be evaluated for each single Data Point of the input Data Set. It 555 
can contain Values of the Value Domains or Variables specified in the Ruleset signature 556 
and constants; all the VTL-ML component level operators are allowed. If omitted then 557 
antecedentCondition is assumed to be TRUE. 558 
consequentCondition a boolean expression to be evaluated for each single Data Point of the input Data Set when 559 
the antecedentCondition evaluates to TRUE (as mentioned, missing antecedent 560 
30 
 
conditions are assumed to be TRUE). It contains Values of the Value Domains or Variables 561 
specified in the Ruleset signature and constants; all the VTL-ML component level 562 
operators are allowed. A consequent condition equal to FALSE is considered as a non-563 
valid result.  564 
errorCode a literal denoting the error code associated to the rule, to be assigned to the possible non-565 
valid results in case the Rule is used for validation. If omitted then no error code is 566 
assigned (NULL value). VTL assumes that a Value Domain errorcode_vd of error codes 567 
exists in the Information Model and contains all possible error codes: the errorCode 568 
literal must be one of the possible Values of such a Value Domain. VTL assumes also that a 569 
Variable errorcode for describing the error codes exists in the IM and is a dependent 570 
variable of the Data Sets which contain the results of the validation.  571 
errorLevel a literal denoting the error level (severity) associated to the  rule, to be assigned to the 572 
possible non-valid results in case the Rule is used for validation. If omitted then no error 573 
level is assigned (NULL value). VTL assumes that a Value Domain errorlevel_vd of error 574 
levels exists in the Information Model and contains all possible error levels: the 575 
errorLevel literal must be one of the possible Values of such a Value Domain. VTL 576 
assumes also that a Variable errorlevel for describing the error levels exists in the IM and 577 
is a dependent variable of the Data Sets which contain the results of the validation.  578 
 579 
Parameters  580 
rulesetName ::   name <ruleset > 581 
valueDomain ::  name < valuedomain > 582 
vdAlias ::  name 583 
variable ::  name 584 
varAlias ::  name 585 
ruleName ::   name 586 
antecedentCondition ::   boolean 587 
consequentCondition ::  boolean 588 
errorCode ::  errorcode_vd 589 
errorLevel ::    errorlevel_vd 590 
 591 
 592 
Constraints 593 
 antecedentCondition and consequentCondition can refer only to the Value Domains or Variables specified 594 
in the dpRulesetSignature. 595 
 Either ruleName is specified for all the Rules of the Ruleset or for none. 596 
 If specified, then ruleName must be unique within the Ruleset. 597 
 598 
Semantic specification 599 
This operator defines a persistent Data Point Ruleset named rulesetName that can be used for validation 600 
purposes.  601 
A Data Point Ruleset is a persistent object that contains Rules to be applied to the Data Points of a Data Set1. The 602 
Data Point Rulesets can be invoked by the check_datapoint operator. The Rules are aimed at checking the 603 
combinations of values of the Data Set Components, assessing if these values fulfil the logical conditions 604 
expressed by the Rules themselves. The Rules are evaluated independently for each Data Point, returning a 605 
Boolean scalar value (i.e., TRUE for valid results and FALSE for non-valid results). 606 
Each Rule contains an (optional) antecedentCondition boolean expression followed by a consequentCondition 607 
boolean expression and expresses a logical implication. Each Rule states that when the antecedentCondition 608 
evaluates to TRUE for a given Data Point, then the consequentCondition is expected to be TRUE as well. If this 609 
implication is fulfilled, the result is considered as valid (TRUE), otherwise as non-valid (FALSE).  On the other 610 
side, if the antecedentCondition evaluates to FALSE, the consequentCondition does not applies and is not 611 
evaluated at all, and the result is considered as valid (TRUE). In case the antecedentCondition is absent then it is 612 
assumed to be always TRUE, therefore the consequentCondition is expected to evaluate to TRUE for all the Data 613 
Points.  See an example below: 614 
 615 
                                                           
1 In order to apply the Ruleset to more Data Sets, these Data Sets must be composed together using the  appropriate VTL 
operators in order to obtain a single Data Set. 
 
31 
 
Rule   Meaning 
On Value Domains: 
when flow_type = "CREDIT" or flow_type = 
"DEBIT" then numeric_value >= 0 
When the Component of the Data Set which is 
defined on the Value Domain named flow_type 
takes the value “CREDIT” or the value “DEBIT”, 
then the other Component defined on the Value 
Domain named numeric_value is expected to 
have a zero or positive value.  
On Variables: 
when flow = "CREDIT" or flow = "DEBIT" then  
obs_value >= 0 
When the Component of the Data Set named 
flow has the value “CREDIT” or “DEBIT” then the 
Component named obs_value is expected to 
have a value greater than zero. 
 616 
The definition of a Ruleset comprises a signature (dpRulesetSignature), which specifies the Value Domains or 617 
Variables on which the Ruleset is defined and a set of Rules, that are the Boolean expressions to be applied to 618 
each Data Point. The antecedentCondition and consequentCondition of the Rules can refer only to the Value 619 
Domains or Variables of the Ruleset signature.   620 
The Value Domains or the Variables of the Ruleset signature identify the space in which the rules are defined 621 
while each Rule provides for a criterion that demarcates the Set of valid combinations of Values inside this space. 622 
The Data Point Rulesets can be defined in terms of Value Domains in order to maximize their reusability, in fact 623 
this way a Ruleset can be applied on any Data Set which has Components which take values on the Value 624 
Domains of the Ruleset signature.  The association between the Components of the Data Set and the Value 625 
Domains of the Ruleset signature is provided by the check_datapoint operator at the invocation of the Ruleset.  626 
When the Ruleset is defined on Variables, their reusability is intentionally limited to the Data Sets which contains 627 
such Variables (and not to other possible Variables which take values from the same Value Domain). If at a later 628 
stage the Ruleset would need to be applied also to other Variables defined on the same Value Domain, a similar  629 
Ruleset should be defined also for the other Variable. 630 
Rules are uniquely identified by ruleName. If omitted then ruleName is implicitly assumed to be the progressive 631 
order number of the Rule in the Ruleset. Please note however that, using this default mechanism, the Rule Name 632 
can change if the Ruleset is modified, e.g., if new Rules are added or existing Rules are deleted, and therefore the 633 
users that interpret the validation results must be aware of these changes. In addition, if the results of more than 634 
one Ruleset have to be combined in one Data Set, then the user should make the relevant rulesetNames different. 635 
As said, each Rule is applied in a row-wise fashion to each individual Data Point of a Data Set. The references to 636 
the Value Domains defined in the antecedentCondition and consequentCondition are replaced with the values 637 
of the respective Components of the Data Point under evaluation.  638 
. 639 
 640 
Examples 641 
 642 
define datapoint ruleset DPR_1 ( valuedomain flow_type  A, numeric_value B ) is 643 
 when A = “CREDIT” or A = “DEBIT” then B >= 0 errorcode “Bad value” errorlevel 10 644 
end datapoint ruleset 645 
 646 
define datapoint ruleset DPR_2 ( variable flow F, obs_value O) is 647 
 when F = “CREDIT” or F = “DEBIT” then O >= 0 errorcode “Bad value” 648 
end datapoint ruleset 649 
define hierarchical ruleset 650 
 651 
Semantics 652 
32 
 
This operator defines a persistent Hierarchical Ruleset that contains Rules to be applied to individual 653 
Components of a given Data Set in order to make validations or calculations according to hierarchical 654 
relationships between the relevant Code Items. These Rulesets are also called “vertical” taking into account  the 655 
tabular representation of a Data Set (considered as a mathematical function), in which each (vertical) column 656 
represents a variable and each (horizontal) row represents a Data Point: these Rulesets are applied on variables 657 
(columns), i.e., vertically on the tabular representation of a Data Set. 658 
A main purpose of the hierarchical Rules is to express some more aggregated Code Items (e.g. the continents) in 659 
terms of less aggregated ones (e.g., their countries) by using Code Item Relationships.  This kind of relations can 660 
be applied to aggregate data, for example to calculate an additive measure (e.g., the population) for the 661 
aggregated Code Items (e.g., the continents) as the sum of the corresponding measures of the less aggregated 662 
ones (e.g., their countries). These rules can be used also for validation, for example to check if the additive 663 
measures relevant to the aggregated Code Items (e.g., the continents) match the sum of the corresponding 664 
measures of their component Code Items (e.g., their countries), provided that the input Data Set contains all of 665 
them, i.e. the more and the less aggregated Code Items. 666 
Another purpose of these Rules is to express the relationships in which a Code Item represents some part of 667 
another one, (e.g., “Africa” and “Five largest countries of Africa”, being the latter a detail of the former). This kind 668 
of relationships can be used only for validation, for example to check if a positive and additive measure (e.g., the 669 
population) relevant to the more aggregated Code Item (e.g., Africa)  is greater than the corresponding measure 670 
of the other more detailed one (e.g., “5 largest countries of Africa”).  671 
The name “hierarchical” comes from the fact that this kind of Ruleset is able to express the hierarchical 672 
relationships between Code Items at different levels of detail, in which each (aggregated) Code Item is expressed 673 
as a partition of (disaggregated) ones. These relationships can be recursive, i.e., the aggregated Code Items can 674 
be in their turn component of even more aggregated ones, without limitations about the number of recursions. 675 
As a first simple example, the following Hierarchical Ruleset named “BeneluxCountriesHierarchy” contains a 676 
single rule that asserts that, in the Value Domain “Geo_Area”, the Code Item BENELUX is the aggregation of the 677 
Code Items BELGIUM, LUXEMBOURG  and NETHERLANDS: 678 
define hierarchical ruleset  BeneluxCountriesHierarchy (valuedomain rule Geo_Area ) is  679 
BENELUX = BELGIUM + LUXEMBOURG + NETHERLANDS   680 
end hierarchical ruleset 681 
 682 
Syntax 683 
 684 
define  hierarchical ruleset    rulesetName    ( hrRulesetSignature )   is  685 
hrRule  686 
{ ; hrRule }* 687 
end hierarchical ruleset 688 
 689 
hrRulesetSignature  ::= vdRulesetSignature | varRulesetSignature  690 
vdRulesetSignature ::= valuedomain { condition vdConditioningSignature } rule ruleValueDomain 691 
vdConditioningSignature ::= condValueDomain { as vdAlias } { , condValueDomain { as vdAlias } }* 692 
varRulesetSignature ::= variable { condition varConditioningSignature } rule ruleVariable 693 
varConditioningSignature ::= condVariable { as vdAlias } { , condVariable { as vdAlias } }* 694 
hrRule ::= { ruleName : } codeItemRelation { errorcode errorCode } { errorlevel errorLevel } 695 
codeItemRelation  ::=   696 
{ when  leftCondition  then }    697 
leftCodeItem    {  =  |  >  |  <  |  >=  |  <=  }1     698 
{  + | -  }  rightCodeItem  { [ rightCondition ] } 699 
{  {  + | -  }1  rightCodeItem   { [ rightCondition ] } }* 700 
 701 
Syntax description 702 
 703 
rulesetName  the name of the Hierarchical Ruleset to be defined. 704 
hrRulesetSignature  the signature of the Ruleset. It specifies the Value Domain or Variable on which the 705 
Ruleset is defined, and the Conditioning Signature. 706 
vdRulesetSignature  the signature of a Ruleset defined on Value Domains 707 
varRulesetSignature  the signature of a Ruleset defined on Variables 708 
hrRule  a single hierarchical rule, as described below. 709 
33 
 
vdConditioningSignature  specifies the Value Domains on which the conditions are defined. The Ruleset is meant 710 
to be applicable to the Data Sets having  Components that take values on the Value 711 
Domain on which the ruleset is defined (i.e., ruleValueDomain) and on the 712 
conditioning Value Domains (i.e.,  condValueDomain).  713 
ruleValueDomain the Value Domain on which the Ruleset is defined 714 
condValueDomain a conditioning Value Domain of the Ruleset  715 
vdAlias   an (optional) alias assigned to a Value Domain and valid only within the Ruleset, this 716 
can be used  for the sake of compactness in writing leftCondition and rightCondition. If 717 
an alias is not specified then the name of the Value Domain  (i.e.,  condValueDomain) 718 
must be used. 719 
varConditioningSignature the signature of the (possible) conditions of the Ruleset defined on Variables. It 720 
specifies the Represented Variables (see the information model) on which these 721 
conditions are defined. The Ruleset is meant to be applicable to any Data Set having 722 
Components which are defined by the Variable on which the Ruleset is expressed (i.e., 723 
variable) and on the Conditioning Variables.  724 
ruleVariable  the variable on which the Ruleset is defined   725 
condVariable a conditioning Variable of the Ruleset  726 
varAlias   an (optional) alias assigned to a Variable and valid only within the Ruleset, this can be 727 
used  for the sake of compactness in writing leftCondition and rightCondition. If an 728 
alias is not specified then the name of the Variableomain  (parameter condVariable) 729 
must be used. 730 
ruleName  the name assigned to the specific Rule within the Ruleset. If the Ruleset is used for 731 
validation then the ruleName identifies the validation results of the various Rules of 732 
the Ruleset.  The ruleName is optional and, if not specified, is assumed to be the 733 
progressive order number of the Rule in the Ruleset. However please note that, if 734 
ruleName is omitted, then the Rule names can change in case the Ruleset is modified, 735 
e.g., if new Rules are added or existing Rules are deleted, and therefore the users that 736 
interpret the validation results must be aware of these changes. In addition, if the 737 
results of more than one Ruleset have to be combined in one Data Set, then the user 738 
should make the relevant rulesetNames different. 739 
codeItemRelation  specifies a (possibly conditioned) Code Item Relation. It expresses a logical relation 740 
between Code Items belonging to the Value Domain of the hrRulesetSignature, 741 
possibly conditioned by the Values of the Value Domains or Variables of the 742 
Conditioning Signature. The relation is expressed by one of the symbols =, >, >=, <, <=, 743 
that in this context denote special logical relationships typical of Code Items. The first 744 
member of the relation is a single Code Item. The second member of the relationship 745 
is the composition of one or more Code Items combined using the symbols + or -, 746 
which in turn also denote special logical operators typical of Code Items. The meaning 747 
of these symbols is better explained below and in the User Manual.  748 
errorCode  a literal denoting the error code associated to the rule, to be assigned to the possible 749 
non-valid results in case the Rule is used for validation. If omitted then no error code 750 
is assigned (NULL value). VTL assumes that a Value Domain errorcode_vd of the error 751 
codes exists in the Information Model and contains all the possible error codes: the 752 
errorCode literal must be one of the possible Values of such a Value Domain. VTL 753 
assumes also that a Variable errorcode for describing the error codes exists in the IM 754 
and is a dependent variable of the Data Sets which contain the results of the 755 
validation.  756 
errorLevel  a literal denoting the error level (severity) associated to the  rule, to be assigned to the 757 
possible non-valid results in case the Rule is used for validation. If omitted then no 758 
error level is assigned (NULL value).  VTL assumes that a Value Domain errorlevel_vd 759 
of the error levels exists in the Information Model and contains all the possible error 760 
levels: the errorLevel literal must be one of the possible Values of such a Value 761 
Domain. VTL assumes also that a Variable errorlevel for describing the error levels 762 
exists in the IM and is a dependent variable of the Data Sets which contain the results 763 
of the validation.  764 
leftCondition  a boolean expression which defines the pre-condition for evaluating the left member 765 
Code Item (i.e., it is evaluated only when the leftCondition is TRUE); It can contain 766 
references to the Value domains or the Variables of the conditioningSignature of the 767 
Ruleset and Constants; all the VTL-ML  component level operators are allowed. The 768 
34 
 
leftCondition is optional, if missing it is assumed to be TRUE and the Rule is always 769 
evaluated. 770 
leftCodeItem  a Code Item of the Value Domain specified in the hrRulesetSignature. 771 
rightCodeItem a Code Item of the Value Domain specified in the hrRulesetSignature. 772 
rightCondition  a boolean scalar expression which defines the condition for a right member Code Item 773 
to contribute to the evaluation of the Rule (i.e., the right member Code Item is taken 774 
into account only when the relevant rightCondition is TRUE). It can contain references 775 
to the Value Domains or Variables of the vdConditioningSignature or 776 
varConditioningSignature of the Ruleset and Constants; all the VTL-ML component 777 
level operators are allowed. The rightCondition is optional, if omitted then it is 778 
assumed to be TRUE and the right member Code Item is always taken into account.   779 
 780 
Input parameters type 781 
 782 
rulesetName ::   name < ruleset > 783 
ruleValueDomain ::  name <valuedomain > 784 
condValueDomain ::  name <valuedomain > 785 
vdAlias ::   name 786 
ruleVariable ::    name  787 
condVariable ::   name  788 
varAlias ::   name 789 
ruleName ::  name  790 
errorCode ::  errorcode_vd  791 
errorLevel ::  errorlevel_vd  792 
leftCondition ::  boolean 793 
leftCodeItem ::  name  794 
rightCodeItem  ::     name 795 
rightCondition ::  boolean 796 
 797 
Constraints 798 
 leftCondition and rightCondition can refer only to Value Domains or Variables specified in 799 
vdConditioningSignature or varConditioningSignature. 800 
 Either the ruleName is specified for all the Rules of the Ruleset or for none. 801 
 If specified, the ruleName must be unique within the Ruleset. 802 
 803 
Semantic specification 804 
This operator defines a Hierarchical Ruleset named rulesetName that can be used both for validation and 805 
calculation purposes (see check_hierarchy and hierarchy). A Hierarchical Ruleset is a set of Rules expressing 806 
logical relationships between the Values (Code Items) of a Value Domain or a Represented Variable.   807 
Each rule contains a Code Item Relation, possibly conditioned, which expresses the relation between Code 808 
Items to be enforced. In the relation, the left member Code Item is put in relation to a combination of one or 809 
more right member Code Items.  The kinds of relations are described below. 810 
The left member Code Item can be optionally conditioned through a leftCondition, a boolean expression which 811 
defines the cases in which the Rule has to be applied (if not declared the Rule is applied ever). The participation 812 
of each right member Code Item in the Relation can be optionally conditioned through a rightCondition, a 813 
boolean expression which defines the cases in which the Code Item participates in the relation (if not declared 814 
the Code Item participates to the relation ever). 815 
As for the mathematical meaning of the relation, please note that each Value (Code Item) is the representation of 816 
an event belonging to a space of events (i.e., the relevant Value Domain), according to the notions of “event” and 817 
“space of events” of the probability theory (see also the section on the Generic Models for Variables and Value 818 
Domains in the VTL IM). Therefore the relations between Values (Code Items) express logical implications 819 
between events. 820 
The envisaged types of relations are: “coincides” (=), “implies” (<), “implies or coincides” (<=), “is implied by” 821 
(>), “is implied by or coincides” (>=)2.  For example: 822 
UnitedKingdom < Europe   823 
means that UnitedKingdom implies Europe (if a point belongs to United Kingdom it also belongs to Europe). 824 
January2000 <  year2000   825 
                                                           
2 “Coincides” means  “implies and is implied” 
35 
 
means that January of the year 2000 implies the year 2000 (if a time instant belongs to “January 2000” it also 826 
belongs to the “year 2000”) 827 
The first member of a Relation is a single Code Item. The second member can be either a single Code Item, like in 828 
the example above, or a logical composition of Code Items giving another Code Item as result. The logical 829 
composition can be defined by means of Code Item Operators, whose goal is to compose some Code Items in 830 
order to obtain another Code Item.  831 
Please note that the symbols + and - do not denote the usual operations of sum and subtraction, but logical 832 
operations between Code Items which are seen as events of the probability theory. In other words, two or more 833 
Code Items cannot be summed or subtracted to obtain another Code Item, because they are events and not 834 
numbers, however they can be manipulated through logical operations like “OR” and  “Complement”.  835 
Note also that the + also acts as a declaration that all the Code Items denoted by + in the formula are mutually 836 
exclusive one another (i.e., the corresponding events cannot happen at the same time), as well as the - acts as a 837 
declaration that all the Code Items denoted by - in the formula are mutually exclusive one another and 838 
furthermore that each one of them is a part of (implies) the result of the composition of all the Code Items having 839 
the + sign. 840 
At intuitive level, the symbol + means “with” (Benelux = Belgium with Luxembourg with Netherland) while the 841 
symbol - means “without” (EUwithoutUK = EuropeanUnion without UnitedKingdom).    842 
When these relationships are applied to additive numeric measures (e.g., the population relevant to geographical 843 
areas), they allow to obtain the measure values of the compound Code Items (i.e., the population of Benelux and 844 
EUwithoutUK) by summing or subtracting the measure values relevant to the component Code Items   (i.e., the 845 
population of Belgium, Luxembourg and Netherland). This is why these logical operations are denoted in VTL 846 
through the same symbols as the usual sum and subtraction. Please note also that this property is valid 847 
whichever is the Data Set and whichever is the additive measure (provided that the possible other Identifier 848 
Components of the Data Set Structure have the same values), therefore the Rulesets of this kind are potentially 849 
largely reusable.   850 
The Ruleset Signature specifies the space on which the Ruleset is defined, i.e., the ValueDomain or Variable on 851 
which the Code Item Relations  are defined (the Ruleset is meant to be applicable to Data Sets having a 852 
Component which takes values on such a Value Domain or are defined by such a Variable). The optional 853 
vdConditioningSignature specifies the conditioning Value Domains (the conditions can refer only to those Value 854 
Domains), as well as the optional varConditioningSignature specifies the conditioning  Variables  (the conditions 855 
can refer only to those Variables).   856 
The Hierarchical Ruleset may act on one or more Measures of the input Data Set provided that these measures 857 
are additive (for example it cannot be applied on a measure containing a “mean” because it is not additive). 858 
Within the Hierarchical Rulesets there can be dependencies between Rules, because the inputs of some Rules can 859 
be the output of other Rules, so the former can be evaluated only after the latter. For example, the data relevant 860 
to the Continents can be calculated only after the calculation of the data relevant to the Countries. As a 861 
consequence, the order of calculation of the Rules is determined by their mutual dependencies and can be 862 
different from the order in which the Rules are written in the Ruleset. The dependencies between the Rules form 863 
a directed acyclic graph. 864 
The Hierarchical ruleset can be used for calculations  to calculate the upper levels of the hierarchy if the data 865 
relevant to the leaves (or some other intermediate level) are available in the operand Data Set of the hierarchy 866 
operator (for more information see also the “Hierarchy” operator). For example, having additive Measures 867 
broken by region, it would be possible to calculate these Measures broken by countries, continents and the 868 
world. Besides, having additive Measures broken by country, it would be possible to calculate the same Measures 869 
broken by continents and the world. 870 
When a Hierarchical Ruleset is used for calculation, only the Relations expressing coincidence (=) are evaluated 871 
(provided that the leftCondition is TRUE, and taking into account only right-side Code Items whose 872 
rightCondition is TRUE). The result Data Set will contain the compound Code Items (the left members of those 873 
relations) calculated from the component Code Items (the right member of those Relations), which are taken 874 
from the input Data Set (for more details about the evaluation options see the hierarchy operator). Moreover, 875 
the clauses typical of the validation are ignored (e.g., ErrorCode, ErrorLevel).  876 
The Hierarchical Ruleset can be also used to filter the input Data Points. In fact if some Code Items are defined 877 
equal to themselves, the relevant Data Points are brought in the result unchanged. For example, the following 878 
Ruleset will maintain in the result the Data Points of the input Data Set relevant to Belgium, Luxembourg and 879 
Netherland and will add new Data Points containing the calculated value for Benelux: 880 
 881 
define hierarchical ruleset BeneluxRuleset ( valuedomain rule GeoArea) is  882 
  Belgium = Belgium 883 
; Luxembourg = Luxembourg 884 
; Netherlands = Netherlands  885 
36 
 
; Benelux = Belgium + Luxembourg + Netherlands 886 
end hierarchical ruleset 887 
 888 
The Hierarchical Rulesets can be used for validation in case various levels of detail are contained in the Data 889 
Set to be validated (see also the check_hierarchy operator for more details).  The Hierarchical Rulesets express 890 
the coherency Rules between the different levels of detail. Because in the validation the various Rules can be 891 
evaluated independently, their order is not significant.  892 
If a Hierarchical Ruleset is used for validation, all the possible Relations (=, >, >=, <, <=) are evaluated (provided 893 
that the leftCondition is TRUE and taking into account only right-side Code Items whose rightCondition is TRUE). 894 
The Rules are evaluated independently. Both the Code Items of the left and right members of the Relations are 895 
expected to belong to and taken from the input Data Set (for more details about the evaluation options see the 896 
check_hierarchy operator). The Antecedent Condition is evaluated and, if TRUE, the operations specified in the 897 
right member of the Relation are performed and the result is compared to the first member, according to the 898 
specified type of Relation. The possible relations in which Code Items are defined as equal to themselves are 899 
ignored. Further details are described in the check_hierarchy operator. 900 
If the data to be validated are in different Data Sets, either they can be joined in advance using the proper VTL 901 
operators or the validation can be done by comparing those Data Sets directly, without using a Hierarchical 902 
Ruleset (see also the check  operator). 903 
 904 
Through the right and left Conditions, the Hierarchical Rulesets allow to declare the time validity of 905 
Rules and Relations. In fact leftCondition and RightCondition can be defined in term of the time Value Domain, 906 
expressing respectively when the left member Code Item has to be evaluated (i.e., when it is considered valid)  907 
and when a right member Code Item participates in the relation.   908 
The following two simplified examples show possible ways of defining the European Union in term of 909 
participating Countries. 910 
Example 1   (for simplicity the time literals are written without the needed “cast” operation) 911 
define hierarchical ruleset  EuropeanUnionAreaCountries1  912 
( valuedomain condition ReferenceTime as Time rule GeoArea ) is  913 
  when between (Time, “1.1.1958”, “31.12.1972”) 914 
then EU = BE + FR + DE + IT + LU + NL 915 
; when between (Time, “1.1.1973”, “31.12.1980”) 916 
then EU = … same as above … + DK + IE + GB 917 
; when between (Time, “1.1.1981”,  “02.10.1985”) 918 
then EU = … same as above … + GR 919 
; when between (Time, “1.1.1986”,  “31.12.1994”) 920 
then EU = … same as above … + ES + PT 921 
; when between (Time, “1.1.1995”,  “30.04.2004”) 922 
then EU = … same as above … + AT + FI + SE 923 
; when between (Time, “1.5.2004”, “31.12.2006”) 924 
then EU = … same as above … +CY+CZ+EE+HU+LT+LV+MT+PL+SI+SK 925 
; when between (Time, “1.1.2007”,  “30.06.2013”) 926 
then EU = … same as above … + BG + RO 927 
; when >= “1.7.2013” 928 
then EU = … same as above … + HR 929 
end hierarchical ruleset 930 
Example 2   (for simplicity the time literals are written without the needed “cast” operation) 931 
define hierarchical ruleset  EuropeanUnionAreaCountries2  932 
(valuedomain condition ReferenceTime as Time rule GeoArea )  is  933 
EU =     AT  [ Time >= “0101.1995” ]   934 
+ BE [ Time >= “01.01.1958” ]  935 
+ BG [ Time >= “01.01.2007” ]  936 
           937 
+  …  938 
           + SE [ Time >= “01.01.1995” ]  939 
+ SI [ Time >= “01.05.2004” ]  940 
+ SK [ Time >= “01.05.2004” ] 941 
end hierarchical ruleset 942 
37 
 
The Hierarchical Rulesets allow defining hierarchies either having or not having levels (free hierarchies). 943 
For example, leaving aside the time validity for sake of simplicity: 944 
define hierarchical ruleset  GeoHierarchy ( valuedomain rule Geo_Area) is  945 
  World = Africa + America + Asia + Europe + Oceania  946 
; Africa = Algeria + … + Zimbabwe 947 
; America = Argentina + … + Venezuela 948 
; Asia = Afghanistan + … + Yemen 949 
; Europe = Albania + … + VaticanCity 950 
; Oceania = Australia + … +  Vanuatu 951 
; Afghanistan = AF_reg_01 + … + AF_reg_N 952 
   … … … … … … 953 
; Zimbabwe = ZW_reg_01 +  …  +  ZW_reg_M  954 
; EuropeanUnion = … + … + … + … 955 
; CentralAmericaCommonMarket = … + … + … + … 956 
; OECD_Area = … + … + … + … 957 
end hierarchical ruleset 958 
The Hierarchical Rulesets allow defining multiple relations for the same Code Item. 959 
Multiple relations are often useful for validation. For example, the Balance of Payments item "Transport" can be 960 
broken down both by type of carrier (Air transport, Sea transport, Land transport) and by type of objects 961 
transported (Passengers and Freights) and both breakdowns must sum up to the whole "Transport" figure. In 962 
the following example a RuleName is assigned to the different methods of breaking down the Transport. 963 
 964 
define hierarchical ruleset  TransportBreakdown ( variable rule BoPItem )  is  965 
  transport_method1 :  Transport  =  AirTransport + SeaTransport + LandTransport 966 
; transport_method2 : Transport = PassengersTransport + FreightsTransport 967 
end hierarchical ruleset 968 
 969 
Multiple relations can be useful even for calculation. For example, imagine that the input Data Set contains data 970 
about resident units broken down by region and data about non-residents units broken down by country. In 971 
order to calculate a homogeneous level of aggregation (e.g., by country), a possible Ruleset is the following: 972 
 973 
define hierarchical ruleset  CalcCountryLevel ( valuedomain condition Residence rule GeoArea) is  974 
  when Residence = “resident” then Country1  = Country1  975 
; when Residence = “non-resident” then Country1 = Region11 + … + Region1M 976 
  … 977 
; when Residence = “resident” then CountryN = CountryN 978 
; when Residence = “non-resident” then CountryN = Region N1 + … + RegionNM 979 
end hierarchical ruleset  980 
 981 
In the calculation, basically, for each Rule, for all the input Data Points and provided that the conditions are 982 
TRUE, the right Code Items are changed into the corresponding left Code Item, obtaining Data Points referred 983 
only to the left Code Items. Then the outcomes of all the Rules of the Ruleset are aggregated together to obtain 984 
the Data Points of the result Data Set. 985 
As far as each left Code Item is calculated by means of a single Rule (i.e., a single calculation method), this 986 
process cannot generate inconsistencies.  987 
Instead if a left Code Item is calculated by means of more Rules (e.g., through more than one calculation method), 988 
there is the risk of producing erroneous results (e.g., duplicated data), because the outcome of the multiple Rules 989 
producing the same Code Item are aggregated together. Proper definition of the left or right conditions can avoid 990 
this risk, ensuring that for each input Data Point just one Rule is applied. 991 
If the Ruleset is aimed only at validation, there is no risk of producing erroneous results because in the validation 992 
the rules are applied independently.  993 
 994 
Examples  995 
1) The Hierarchical Ruleset is defined on the Value Domain “sex”: Total is defined as Male + Female.  996 
 No  conditions are defined. 997 
 998 
define hierarchical ruleset sex_hr  (valuedomain rule sex)  is 999 
 TOTAL = MALE + FEMALE 1000 
end hierarchical ruleset  1001 
 1002 
38 
 
2) BENELUX is the aggregation of the Code Items BELGIUM, LUXEMBOURG and NETHERLANDS. No conditions 1003 
are defined. 1004 
 1005 
define hierarchical ruleset  BeneluxCountriesHierarchy (valuedomain rule GeoArea) is  1006 
BENELUX = BELGIUM + LUXEMBOURG + NETHERLANDS errorcode “Bad value for Benelux”  1007 
end hierarchical ruleset 1008 
 1009 
3) American economic partners. The first rule states that the value for North America should be greater than the 1010 
value reported for US. This type of validation is useful when the data communicated by the data provider do not 1011 
cover the whole composition of the aggregate but only some elements. No conditions are defined. 1012 
 1013 
define hierarchical ruleset american_partners_hr (variable rule PartnerArea) is 1014 
  NORTH_AMERICA > US  1015 
; SOUTH_AMERICA = BR + UY + AR + CL  1016 
end hierarchical ruleset 1017 
 1018 
4) Example of an aggregate Code Item having multiple definitions to be used for validation only. The Balance of 1019 
Payments item "Transport" can be broken down by type of carrier (Air transport, Sea transport, Land transport) 1020 
and by type of objects transported (Passengers and Freights) and both breakdowns must sum up to the total 1021 
"Transport" figure. 1022 
 1023 
define hierarchical ruleset validationruleset_bop (variable rule BoPItem ) is 1024 
   transport_method1 : Transport  =  AirTransport + SeaTransport + LandTransport  1025 
;  transport_method2 : Transport  =  PassengersTransport + FreightsTransport 1026 
end hierarchical ruleset 1027 
 1028 
 1029 
39 
 
VTL-DL – User Defined Operators  1030 
define operator 1031 
Syntax 1032 
define operator  operator_name ( { parameter { , parameter }* } ) 1033 
{ returns outputType } 1034 
is operatorBody 1035 
end define operator 1036 
 1037 
parameter::= parameterName parameterType { default parameterDefaultValue } 1038 
 1039 
Syntax description 1040 
operator_name   the name of the operator 1041 
parameter the names of parameters, their data types  and  defaultvalues 1042 
outputType   the  data type of the artefact returned by the operator 1043 
operatorBody the expression which defines the operation  1044 
parameterName the name of the parameter 1045 
parameterType the data type of the parameter 1046 
parameterDefaultValue the default value for the parameter (optional) 1047 
  1048 
Parameters 1049 
operator_name   name 1050 
outputType   a VTL  data type (see the Data Type Syntax below) 1051 
operatorBody a VTL expression having the parameters (i.e., parameterName) as the operands  1052 
parameterName name 1053 
parameterType a VTL data type (see the Data Type Syntax below) 1054 
parameterDefaultValue a Value of the same type as the parameter 1055 
   1056 
Constraints 1057 
 Each parameterName  must be unique within the list of parameters 1058 
 parameterDefaultValue must be of the same data type as the corresponding parameter 1059 
 outputType must be compatible with the type of operatorBody (it can also be a sub-type of the type returned 1060 
by the operatorBody expression) 1061 
 If outputType is omitted then the type returned by the operatorBody expression is assumed 1062 
 If parameterDefaultValue is specified then the parameter is optional 1063 
 1064 
Semantic specification 1065 
This operator defines a user-defined Operator by means of a VTL expression, specifying also the parameters, 1066 
their data types, whether they are mandatory or optional and their (possible) default values.  1067 
 1068 
Examples 1069 
Example1:  1070 
define operator max1 (x integer, y integer) 1071 
returns boolean is  1072 
if x > y then x else y 1073 
end define operator 1074 
 1075 
Example2: 1076 
define operator add (x integer default 0, y integer default 0) 1077 
returns number is  1078 
x+y 1079 
end define operator 1080 
40 
 
Data type syntax 1081 
The VTL data types are described in the VTL User Manual. Types are used throughout this Reference Manual as 1082 
both meta-syntax and syntax.  1083 
They are used as meta-syntax in order to define the types of input and output parameters in the descriptions of 1084 
VTL operators; they are used in the syntax, and thus are proper part of the VTL, in order to allow other operators 1085 
to refer to specific data types. For example, when defining a custom operator (see the define operator above), 1086 
one will need to declare the type of the input/output parameters.  1087 
The syntax of the data types is described below  (as for the meaning of these definitions, see the section VTL Data 1088 
Types  in the User Manual).  See also the section “Conventions for describing the operators’ syntax” in the chapter  1089 
“Overview of the language and conventions” above. 1090 
dataType ::= scalarType | compoundType  1091 
 1092 
scalarType ::=  { basicScalarType | valueDomainName | setName }1 { scalarTypeConstraint } { null | 1093 
not null } 1094 
basicScalarType ::=  { scalar | number | integer | string | boolean | time | date | time_period | 1095 
duration }1  1096 
 valueDomainName ::  name 1097 
 setName ::   name 1098 
scalarTypeConstraint ::= [ valueBooleanCondition ] | { scalarLiteral { , scalarLiteral }* }   1099 
compoundType ::=  componentType | datasetType | operatorType  | rulesetType | productType | 1100 
universalSetType  1101 
componentType ::=   componentRole  { < scalar type > } 1102 
componentRole ::=  { component | identifier | measure | attribute | viral attribute }1 1103 
datasetType ::=    dataset { componentConstraint  { , componentConstraint  }* }  1104 
componentConstraint ::=  componentType  { componentName |  multiplicityModifier }1 1105 
componentName ::  name  1106 
multiplicityModifier ::=   _ { + | * } 1107 
productType ::=    { dataType  { * dataType }+  }1 1108 
operatorType ::=   { dataType  ->  dataType }1 1109 
rulesetType ::=   { ruleset | dpRuleset | hrRuleset }1 1110 
dpRuleset ::=   datapoint  1111 
    | datapoint_on_valuedomains { (  name { * name }* )  } 1112 
    | datapoint_on_variables { (  name { * name }* )  } 1113 
hrRuleset ::=  hierarchical  1114 
| hierarchical_on_valuedomains { valueDomainName  { *  1115 
 ( prodValueDomains )  }  } 1116 
    | hierarchical_on_variables { variableName { * ( prodVariables ) }  } 1117 
universalSetType ::=  set { < dataType > } 1118 
 1119 
Note that the valueBooleanCondition in scalarTypeConstraint is expressed with reference to the fictitious 1120 
variable “value” (see also the User Manual, section  “Conventions for describing the Scalar Types”), which 1121 
represents the generic value of the scalar type, for example: 1122 
integer { 0, 1 }    means an integer number whose value is 0 or 1 1123 
number [ value >= 0 ]  means a number greater or equal than 0 1124 
string { "A", "B", "C" }  means a string whose value is A, B or C: 1125 
41 
 
string [ length (value) <= 10 ] means a string whose length is lower or equal than 10: 1126 
  1127 
General examples of the syntax for defining types can be found in the User Manual, section VTL Data Types and 1128 
in the declaration of the data types of the VTL operators (sub-sections “input parameters type” and “result 1129 
type”).   1130 
42 
 
VTL-ML - Typical behaviours of the ML Operators 1131 
In this section, the common behaviours of some class of VTL-ML operators are described, both for a better 1132 
understanding of the characteristics of such classes and to factor out and not repeat the explanation for each 1133 
operator of the class.  1134 
Typical behaviour of most ML Operators  1135 
Unless differently specified in the Operator description, the Operators can be applied to Scalar Values, to Data 1136 
Sets and to Data Set Components.  1137 
The operations on Scalar Values are primitive and are part of the core of the language. The other kind of 1138 
operations can be typically be obtained by means of the scalar operations in conjunction with the Join operator, 1139 
which is part of the core too.  1140 
In the operations on Data Set, the Operators are meant to be applied by default only to the values of the 1141 
Measures of the input Data Sets, leaving the Identifiers unchanged. The Attributes follow by default their specific 1142 
propagation rules, which are described in the User Manual.  1143 
In the operations on Components, the Operators are meant to be applied on the specified components of one 1144 
input Data Set, in order to calculate a new component which becomes part of the resulting Data Set. In this case, 1145 
the Attributes can be operated like the Measures. 1146 
Operators applicable on one Scalar Value or Data Set or Data Set 1147 
Component 1148 
 1149 
Operations on Scalar values 1150 
The operator is applied on a scalar value and returns a scalar value.  1151 
 1152 
Operations on Data Sets 1153 
The operator is applied on a Data Set and returns a Data Set. 1154 
For example, using a functional style and denoting the operator with  f ( … ), this can written as: 1155 
DS_r  :=  f ( DS_1 )  1156 
The same operation, using an infix style and denoting the operator as op, can be also written as  1157 
DS_r  :=  op  DS_1  1158 
This means that the operator is applied to the values of all the Measures of DS_1 in order to produce 1159 
homonymous Measures in  DS_r. 1160 
The application of the operator is allowed only if all the Measures of the operand Data Set are of a data type 1161 
compatible with the operator (for example, a numeric operator is applicable only if all the Measures of the 1162 
operand Data Sets are numeric). If the Measures of the operand Data Set are of different types, not all compatible 1163 
with the operator to be applied, the membership or the keep clauses can be used to select only the proper 1164 
Measures. No applicability constraints exist on Identifiers and Attributes, which can be any.   1165 
As for the data content, for each Data Point (DP_1) of the operand Data Set, a result Data Point (DP_r) is returned, 1166 
having for the Identifiers the same values as DP_1. 1167 
For each Data Point DP_1 and for each Measure, the operator is applied on the Measure value of DP_1 and 1168 
returns the corresponding Measure value of DP_r.    1169 
For each Data Point DP_1 and for each viral Attribute, the value of the Attribute propagates unchanged in DP_r. 1170 
As for the data structure, the result Data Set (DS_r) has the Identifiers and the Measures of the operand Data Set 1171 
(DS_1), and has the Attributes resulting from the application of the attribute propagation rules on the Attributes 1172 
of the operand Data Set (DS_r maintains the Attributes declared as “viral” in DS_1; these Attributes are 1173 
considered as “viral” also in DS_r, the “non-viral” Attributes of DS_1 are not kept in DS_r). 1174 
 1175 
43 
 
Operations on Data Set Components 1176 
The operator is applied on a Component (COMP_1) of a Data Set (DS_1) and returns another Component 1177 
(COMP_r) which alters the structure of DS_1 in order to produce the result Data Set (DS_r).  1178 
For example, using a functional style and denoting the operator with  f ( … ), this can be written as: 1179 
DS_r := DS_1 [ calc COMP_r :=  f ( COMP_1) ] 1180 
The same operation, using an infix style and denoting the operator as op, can be written as: 1181 
DS_r := DS_1 [ calc COMP_r :=  op  COMP_1 ] 1182 
This means that the operator is applied on COMP_1 in order to calculate COMP_r. 1183 
 If COMP_r is a new Component which originally did not exist in DS_1, it is added to the original Components 1184 
of DS_1, by default as a Measure (unless otherwise specified), in order to produce DS_r.    1185 
 If COMP_r is one of the original Measures or Attributes of DS_1, the values obtained from the application of 1186 
the operator f ( … )  replace the DS_1 original values for such a Measure or Attribute in order to produce 1187 
DS_r. 1188 
 If COMP_r is one of the original Identifiers of DS_1, the operation is not allowed, because the result can 1189 
become inconsistent.  1190 
In any case, an operation on the Components of a Data Set produces a new Data Set, as in the example above.  1191 
The application of the operator is allowed only if the input Component belongs to a data type compatible with 1192 
the operator (for example, a numeric operator is applicable only on numeric Components).  As already said, 1193 
COMP_r cannot have the same name of an Identifier of DS_1. 1194 
As for the data content, for each Data Point DP_1 of DS_1, the operator is applied on the values of COMP_1 so 1195 
returning the value of COMP_r.   1196 
As for the data structure, like for the operations on Data Sets above, the result Data Set (DS_r) has the Identifiers 1197 
and the Measures of the operand Data Set (DS_1), and has the Attributes resulting from the application of the 1198 
attribute propagation rules on the Attributes of the operand Data Set (DS_r maintains the Attributes declared as 1199 
“viral” in DS_1; these Attributes are considered as “viral” also in DS_r, the “non-viral” Attributes of DS_1 are not 1200 
kept in DS_r). If an Attribute is explicitly calculated, the attribute propagation rule is overridden. 1201 
Moreover, in the case of the operations on Data Set Components, the (possible) new Component DS_r can be 1202 
added to the original structure, the role of a (possible) existing DS_1 Component can be altered, the virality of a 1203 
(possibly) existing DS_r Attribute can be altered, a (possible) COMP_r non-viral Attribute can be kept in the 1204 
result. For the alteration of role and virality see also the calc clause. 1205 
Operators applicable on two Scalar Values or Data Sets or Data Set 1206 
Components  1207 
 1208 
Operation on Scalar values 1209 
The operator is applied on two Scalar values and returns a Scalar value.  1210 
 1211 
Operation on Data Sets 1212 
The operator is applied either on two Data Sets or on one Data Set and one Scalar value and returns a Data Set. 1213 
The composition of a Data Set and a Component is not allowed (it makes no sense). 1214 
For example, using a functional style and denoting the operator with  f ( … ), this can be written as: 1215 
DS_r  :=  f ( DS_1, DS_2 )  1216 
The same kind of operation, using an infix stile and denoting the operator as op, can be also written as  1217 
DS_r  :=     DS_1  op   DS_2  1218 
This means that the operator is applied to the values of all the couples of Measures of DS_1 and DS_2 having the 1219 
same names in order to produce homonymous Measures in  DS_r.  DS_1 or DS_2 may be replaced by a Scalar 1220 
value. 1221 
The composition of two Data Sets (DS_1, DS_2) is allowed if the two operand Data Sets have exactly the same 1222 
Measures and if all these Measures belong to a data type compatible with the operator (for example, a numeric 1223 
operator is applicable only if all the Measures of the operand Data Sets are numeric). If the Measures of the 1224 
operand Data Sets are different or of different types not all compatible with the operator to be applied,  the 1225 
membership or the keep clauses can be used to select only the proper Measures.  The composition is allowed if 1226 
44 
 
these operand Data Sets have the same Identifiers or if one of them has at least all the Identifiers of the other one 1227 
(in other words, the Identifiers of one of the Data Sets must be a superset of the Identifiers of the other one). No 1228 
applicability constraints exist on the Attributes, which can be any.   1229 
As for the data content, the operand Data Sets (DS_1, DS_2) are joined to find the couples of Data Points (DP_1, 1230 
DP_2),  where DP_1 is from the first operand (DS_1) and DP_2 from the second operand (DS_2), which have the 1231 
same values as for the common Identifiers. Data Points that are not coupled are left out (the inner join is used). 1232 
An operand Scalar value is treated as a Data Point that couples with all the Data Points of the other operand.  For 1233 
each couple (DP_1, DP_2) a result Data Point (DP_r) is returned, having for the Identifiers the same values as 1234 
DP_1 and DP_2. 1235 
For each Measure and for each couple (DP_1, DP_2), the Measure values of DP_1 and DP_2 are composed through 1236 
the operator so returning the Measure value of DP_r.  An operand Scalar value is composed with all the Measures 1237 
of the other operand.  1238 
For each couple (DP_1, DP_2) and for each Attribute that propagates in DP_r, the Attribute value is calculated by 1239 
applying the proper Attribute propagation algorithm on the values of the Attributes of DP_1 and DP_2 . 1240 
As for the data structure, the result Data Set (DS_r) has all the Identifiers (with no repetition of common 1241 
Identifiers) and the Measures of both the operand Data Sets, and has the Attributes resulting from the 1242 
application of the attribute propagation rules on the Attributes of the operands (DS_r maintains the Attributes 1243 
declared as “viral” for the operand Data Sets; these Attributes are considered as “viral” also in DS_r, the “non-1244 
viral” Attributes of the operand Data Sets  are not kept in DS_r).  1245 
 1246 
Operation on Data Set Components 1247 
The operator is applied either on two Data Set Components (COMP_1, COMP_2) belonging to the same Data Set 1248 
(DS_1) or on a Component and a Scalar value, and returns another Component (COMP_r) which alters the 1249 
structure of DS_1 in order to produce the result Data Set (DS_r). The composition of a Data Set and a Component 1250 
is not allowed (it makes no sense). 1251 
For example, using a functional style and denoting the operator with  f ( … ), this can be written as: 1252 
DS_r := DS_1 [ calc COMP_r :=  f ( COMP_1,  COMP_2 ) ] 1253 
The same operation, using an infix style and denoting the operator as op, can be written as: 1254 
DS_r := DS_1 [ calc COMP_r :=  COMP_1  op   COMP_2 ] 1255 
This means that the operator is applied on COMP_1 and COMP_2 in order to calculate COMP_r. 1256 
 If COMP_r is a new Component which originally did not exist in DS_1, it is added to the original Components 1257 
of DS_1, by default as a Measure (unless otherwise specified), in order to produce DS_r.    1258 
 If COMP_r is one of the original Measures or Attributes of DS_1, the values obtained from the application of 1259 
the operator f ( … )  replace the DS_1 original values for such a Measure or Attribute in order to produce 1260 
DS_r. 1261 
 If COMP_r is one of the original Identifiers of DS_1, the operation is not allowed, because the result can 1262 
become inconsistent.  1263 
In any case, an operation on the Components of a Data Set produces a new Data Set, like in the example above.  1264 
The composition of two Data Set Components is allowed provided that they belong to the same Data Set3. 1265 
Moreover, the input Components must belong to data types compatible with the operator (for example, a 1266 
numeric operator is applicable only on numeric Components).  As already said, COMP_r cannot have the same 1267 
name of an Identifier of DS_1. 1268 
As for the data content, for each Data Point of DS_1, the values of COMP_1 and COMP_2 are composed through 1269 
the operator so returning the value of COMP_r.    1270 
As for the data structure, the result Data Set (DS_r) has the Identifiers and the Measures of the operand Data Set 1271 
(DS_1), and has the Attributes resulting from the application of the attribute propagation rules on the Attributes 1272 
of the operand Data Set (DS_r maintains the Attributes declared as “viral” in DS_1; these Attributes are 1273 
considered as “viral” also in DS_r, the “non-viral” Attributes of DS_1 are not kept in DS_r). If an Attribute is 1274 
explicitly calculated, the attribute propagation rule is overridden. 1275 
Moreover, in the case of the operations on Data Set Components, a (possible) new Component DS_r can be added 1276 
to the original structure of DS_1, the role of a (possibly) existing DS_1 Component can be altered, the virality of a 1277 
                                                           
3 As obvious, the input Data Set can be the result of a previous composition of more other Data Sets, even within the 
same expression 
45 
 
(possibly) existing DS_r Attributes can be altered, a (possible) COMP_r non-viral Attribute can be kept in the 1278 
result. For the alteration of role and virality see also the calc clause. 1279 
Operators applicable on more than two Scalar Values or Data Set 1280 
Components  1281 
The cases in which an operator can be applied on more than two Data Sets (like the Join operators) are described 1282 
in the relevant sections. 1283 
 1284 
Operation on Scalar values 1285 
The operator is applied on more Scalar values and returns a Scalar value  according to its semantics.  1286 
 1287 
Operation on Data Set Components 1288 
The operator is applied either on a combination of more than two Data Set Components (COMP_1, COMP_2) 1289 
belonging to the same Data Set (DS_1) or Scalar values, and returns another Component (COMP_r) which alters 1290 
the structure of DS_1 in order to produce the result Data Set (DS_r). The composition of a Data Set and a 1291 
Component is not allowed (it makes no sense). 1292 
For example, using a functional style and denoting the operator with  f ( … ), this can be written as: 1293 
DS_r := DS_1 [ substr COMP_r :=  f ( COMP_1,  COMP_2, COMP_3 ) ] 1294 
This means that the operator is applied on COMP_1, COMP_2 and COMP_3 in order to calculate COMP_r. 1295 
 If COMP_r is a new Component which originally did not exist in DS_1, it is added to the original Components 1296 
of DS_1, by default as a Measure (unless otherwise specified), in order to produce DS_r.    1297 
 If COMP_r is one of the original Measures or Attributes of DS_1, the values obtained from the application of 1298 
the operator f ( … )  replace the DS_1 original values for such a Measure or Attribute in order to produce 1299 
DS_r. 1300 
 If COMP_r is one of the original Identifiers of DS_1, the operation is not allowed, because the result can 1301 
become inconsistent.  1302 
In any case, an operation on the Components of a Data Set produces a new Data Set, like in the example above.  1303 
The composition of more Data Set Components is allowed provided that they belong to the same Data Set4. 1304 
Moreover, the input Components must belong to data types compatible with the operator (for example, a 1305 
numeric operator is applicable only on numeric Components).  As already said, COMP_r cannot have the same 1306 
name of an Identifier of DS_1. 1307 
As for the data content, for each Data Point of DS_1, the values of COMP_1, COMP_2 and COMP_3 are composed 1308 
through the operator so returning the value of COMP_r.    1309 
As for the data structure, the result Data Set (DS_r) has the Identifiers and the Measures of the operand Data Set 1310 
(DS_1), and has the Attributes resulting from the application of the attribute propagation rules on the Attributes 1311 
of the operand Data Set (DS_r maintains the Attributes declared as “viral” in DS_1; these Attributes are 1312 
considered as “viral” also in DS_r, the “non-viral” Attributes of DS_1 are not kept in DS_r). If an Attribute is 1313 
explicitly calculated, the attribute propagation rule is overridden. 1314 
Moreover, in the case of the operations on Data Set Components, a (possible) new Component DS_r can be added 1315 
to the original structure of DS_1, the role of a (possibly) existing DS_1 Component can be altered, the virality of a 1316 
(possibly) existing DS_r Attributes can be altered, a (possible) COMP_r non-viral Attribute can be kept in the 1317 
result. For the alteration of role and virality see also the calc clause. 1318 
 1319 
Behaviour of Boolean operators  1320 
The Boolean operators are allowed only on operand Data Sets that have a single measure of type boolean. As for 1321 
the other aspects, the behaviour is the same as the operators applicable on one or two Data Sets described above.  1322 
                                                           
4 As obvious, the input Data Set can be the result of a previous composition of more other Data Sets, even within the 
same expression 
46 
 
Behaviour of Set operators 1323 
These operators apply the classical set operations (union, intersection, difference, symmetric differences) to the 1324 
Data Sets, considering them as sets of Data Points.  These operations are possible only if the Data Sets to be 1325 
operated have the same data structure, and therefore the same Identifiers, Measures and Attributes5.  1326 
Behaviour of Time operators  1327 
The time operators are  the operators dealing with time, date and time_period basic scalar types. These types are 1328 
described in the User Manual in the sections “Basic Scalar Types” and “External representations and literals used 1329 
in the VTL Manuals”.  1330 
The time-related formats used for explaining the time operators are the following (they are described also in the 1331 
User Manual). 1332 
For the time values:   1333 
YYYY-MM-DD/YYYY-MM-DD 1334 
Where YYYY are 4 digits for the year, MM two digits for the month, DD two digits for the day.  For 1335 
example: 1336 
2000-01-01/2000-12-31 the whole year 2000 1337 
2000-01-01/2009-12-31 the first decade of the XXI century   1338 
For the date values:   1339 
YYYY-MM-DD 1340 
The meaning of the symbols is the same as above. For example: 1341 
2000-12-31  the 31st December of the year 2000 1342 
2010-01-01  the first of January of the year 2010 1343 
For the time_period values:  1344 
   YYYY{P}{NNN} 1345 
Where YYYY are 4 digits for the year, P is one character for the period indicator of the regular period (it 1346 
refers to the duration data type and can assume one of the possible values listed below), NNN are from 1347 
zero to three digits which contain the progressive number of the period in the year.  For annual data the 1348 
A and the three digits NNN can be omitted. For example: 1349 
2000M12  the month of December of the year 2000 (duration: M) 1350 
2010Q1   the first quarter of the year 2010 (duration: Q) 1351 
2010A   the whole year 2010 (duration: A)  1352 
2010   the whole year 2010 (duration: A)  1353 
For the duration values, which are the possible values of the period indicator of the regular periods above, it is 1354 
used for simplicity just one character whose possible values are the following: 1355 
Code  Duration 1356 
  D  Day 1357 
  W  Week 1358 
  M  Month 1359 
  Q  Quarter  1360 
  S  Semester 1361 
  A  Year 1362 
As mentioned in the User Manual, these are only examples of possible time-related representations, each VTL 1363 
system is free of adopting different ones. In fact no predefined representations are prescribed, VTL systems are 1364 
free to using they preferred or already existing ones. 1365 
Several time operators deal with the specific case of Data Sets of time series, having an Identifier component that 1366 
acts as the reference time and can be of one of the scalar types time, date or time_period; moreover this Identifier 1367 
must be periodical, i.e. its possible values are regularly spaced and therefore have constant duration (frequency). 1368 
                                                           
5 According to the VTL IM, the Variables that have the same name have also the same data type 
47 
 
It is worthwhile to recall here that, in the case of Data Sets of time series, VTL assumes that the information 1369 
about which is the Identifier Components that acts as the reference time and which is the period (frequency) of 1370 
the time series exists and is available in some way in the VTL system. The VTL Operators are aware of which is 1371 
the reference time and the period (frequency) of the time series and use these information to perform correct 1372 
operations. VTL also assumes that a Value Domain representing the possible periods (e.g. the period indicator 1373 
Value Domain shown above) exists and refers to the duration scalar type. For the assumptions above, the users 1374 
do not need to specify which is the Identifier Component having the role of reference time.  1375 
The operators for time series can be applied only on Data Sets of time series and returns a Data Set of time 1376 
series. The result Data Set has the same Identifier, Measure and Attribute Components as the operand Data Set 1377 
and contains the same time series as the operand.  The Attribute propagation rule is not applied. 1378 
Operators changing the data type 1379 
These Operators change the Scalar data type of the operands they are applied to (i.e. the type of the result is 1380 
different from the type of the operand). For example, the length operator is applied to a value of string type and 1381 
returns a value of integer type. Another example is the cast operator. 1382 
 1383 
Operation on Scalar values 1384 
The operator is applied on (one or more) Scalar values and returns one Scalar value of a different data type.   1385 
 1386 
Operation on Data Sets 1387 
If an Operator change the data type of the Variable it is applied to (e.g., from string to number), the result Data Set 1388 
cannot maintain this Variable as it happens in the previous cases, because a Variable cannot have different data 1389 
types in different Data Sets6. 1390 
As a consequence, the converted variable cannot follow the same rules described in the sections above and must 1391 
be replaced, in the result Data Set, by another Variable of the proper data type.   1392 
For sake of simplicity, the operators changing the data type are allowed only on mono-measure operand Data 1393 
Sets, so that the conversion happens on just one Measure. A default generic Measure is assigned by default to the 1394 
result Data Set, depending on the data type of the result (the default Measure Variables are reported in the table 1395 
below). 1396 
Therefore, if the operands are originally multi-measure, just one Measure must be pre-emptively selected (for 1397 
example through the membership operator) in order to apply the changing-type operator. Moreover, if in the 1398 
result Data Set a different Measure Variable name is desired than the one assigned by default, it is possible to 1399 
change the Variable name (see the rename operator). 1400 
As for the Identifiers and the Attributes, the behaviour of these operators is the same as the typical behaviour of 1401 
the unary or binary operators. 1402 
 1403 
Operation on Data Set Components 1404 
For the same reasons above, the result Component cannot be the same as one of the operand Components and 1405 
must be of the appropriate Scalar data type. 1406 
 1407 
Default Names for Variables and Value Domains used in this manual  1408 
The following table shows the default Variable names and the relevant default Value Domain. These are only the 1409 
names used in this manual for explanatory purposes and can be personalised in the implementations. If VTL 1410 
rules are exchanged, the personalised names need to be shared with the partners of the exchange.   1411 
 1412 
Scalar data type Default Variable Default Value Domain 
string string_var string_vd 
                                                           
6 This according both to the mathematical meaning of a Variable and the  VTL Information Model; in fact a 
Represented Variable  is defined on just one Value Domain,  which has just one data type, independently of the Data 
Structures and the Data Sets in which the Variable is used. 
48 
 
number num_var num_vd 
integer int_var int_vd 
time time_var time_vd 
time_period time_period_var time_period_vd 
date date_var date_vd 
duration duration_var duration_vd 
boolean bool_var bool_vd 
Type Conversion and Formatting Mask  1413 
The conversions between scalar types is provided by the operator cast, described in the section of the general 1414 
purpose operators. Some particular types of conversion require the specification of a formatting mask, which 1415 
specifies which format the source or the destination of the conversion should assume. The formatting masks for 1416 
the various scalar types are explained here.   1417 
If needed, the formatting Masks can be personalized in the VTL implementations. If VTL rules are exchanged, the 1418 
personalised masks need to be shared with the partners of the exchange.   1419 
The Numbers Formatting Mask 1420 
The number formatting mask can be defined as a combination of characters whose meaning is the following: 1421 
o “D”   one numeric digit  (if the scientific notation is adopted, D is only for the mantissa)  1422 
o “E”   one numeric digit  (for the exponent of the scientific notation) 1423 
o  “*”    an arbitrary number of digits 1424 
o “+”    at least one digit  1425 
o “.” (dot)  can be used as a separator between the integer and the decimal parts. 1426 
o “,” (comma)  can be used as a separator between the integer and the decimal parts.  1427 
 1428 
Examples of valid masks are: 1429 
 DD.DDDDD, DD.D, D, D.DDDD, D*.D*, D+.D+ , DD.DDDEEEE 1430 
The Time Formatting Mask 1431 
The format of the values of the types time, date and time_period can be specified through specific formatting 1432 
masks.  A mask related to time, date and time_period is formed by a sequence of symbols which denote:  1433 - the time units that are used, for example years, months, days  1434 - the format in which they are represented, for example 4 digits for the year (2018), 2 digits for the month 1435 
within the year (04 for April) and 2 digits for the day within the year and the month (05 for the 5th) 1436 - the order of these parts; for example, first the 4 digits for the year, then the 2 digits for the month and finally 1437 
the 2 digits for the day 1438 - other (possible) typographical characters used in the representation; for example, a line between the year 1439 
and the month and between the month and the day (e.g., 2018-04-05). 1440 
The time formatting masks follows the general rules below. 1441 
For a numerical representations of the time units:  1442 - A digit is denoted through the use of a special character which depends on the time unit. for example Y is 1443 
for “year”, M is for  “month” and D is for “day” 1444 - The special character is lowercase for the time units shorter than the day (for example h for “hour”, m for 1445 
“minute”, s for “second”) and uppercase for time units equal to “day” or longer (for example W for “week”, Q 1446 
for “quarter”, S for “semester”)  1447 
49 
 - The number of  letters matches the number of digits, for example YYYY means that the year is represented 1448 
with four digits and MM that the month is of 2 digits 1449 - The numerical representation is assumed to be padded by leading 0 by default, for example MM means that 1450 
April is represented as 04 and the year 33 AD as 0033 1451 - If the numerical representation is not padded, the optional digits that can be omitted (if equal to zero) are 1452 
enclosed within braces; for example {M}M means that April is represented by 4 and December by 12, while 1453 
{YYY}Y means that the 33 AD is represented by 33 1454 
For textual representations of the time units: 1455 - Special words denote a textual localized representation of a certain unit, for example DAY means a textual 1456 
representation of the day (MONDAY, TUESDAY …) 1457 - An optional number following the special word denote the maximum length, for example DAY3 is a textual 1458 
representation that uses three characters (MON, TUE  …) 1459 - The case of the special word correspond to the case of the value; for example day3 (lowercase) denotes the 1460 
values  mon, tue …  1461 - The case of the initial character of the special word correspond to the case of the initial character of the time 1462 
format; for example Day3 denotes the values  Mon, Tue …  1463 - The letter P denotes the period indicator, (i.e., day, week, month …) and the letter p denotes ond digit for the 1464 
number of periods 1465 
Representation of more time units: 1466 - If more time units are used in the same mask (for example years, months, days), it is assumed that the more 1467 
detailed units (e.g., the day) are expressed through the order number that they assume within the less 1468 
detailed ones (e.g., the month and the year). For example, if years, weeks and days are used, the weeks are 1469 
within the year (from 1 to 53) and the days are within the year and the week (from 1 to 7). 1470 - The position of the digits in the mask denotes the position of the corresponding values; for example, 1471 
YYYMMDD means four digits for the year followed by two digits for the month and then two digits for the 1472 
day (e.g., 20180405 means the year 2018, month April, day 5th) 1473 - Any other character can be used in the mask, meaning simply that it appears in the same position; for 1474 
example, YYYY-MM-DD means that the values of year, month and day are separated by a line (e.g., 2018-1475 
04-05 means the year 2018, month April, day 5th) and \PMM denotes the letter “P” followed by two 1476 
characters for the month. 1477 - The special characters and the special words, if prefixed by the reverse slash (\) in the mask, appear in the 1478 
same position in the time format; for example \PMM\M means the letter “P” followed by two characters for 1479 
the month and then the letter “M”; for example, P03M means a period of three months (this is an ISO 8601 1480 
standard representation for a period of MM months). The reverse slash can appear in the format if needed 1481 
by prefixing it with another reverse slash; for example YYYY\\MM means for digits for the year, a reverse 1482 
slash and two digits for the month.  1483 -  1484 
The special characters and the corresponding time units are the following:  1485 
C century   1486 
Y    year 1487 
S semester   1488 
Q quarter  1489 
M month   1490 
W week  1491 
D day   1492 
h  hour digit  (by default on 24 hours) 1493 
m minute  1494 
s second  1495 
d decimal of second 1496 
P period indicator (see the “duration” codes below) 1497 
p number of periods 1498 
 1499 
The special words for textual representations are the following:  1500 
50 
 
AM/PM  indicator of AM / PM (e.g.  am/pm  for  “am” or “pm”) 1501 
MONTH textual representation of the month (e.g., JANUARY for January) 1502 
DAY   textual representation of the day (e.g., MONDAY for Monday) 1503 
 1504 
Examples of formatting masks for the time scalar type: 1505 
A Scalar Value of type time denotes time intervals of any duration and expressed with any precision, which are 1506 
the intervening time between two time points.  1507 
These examples are about three possible ISO 8601 formats for expressing time intervals: 1508 
 Start and end time points, such as "2015-03-03T09:30:45Z/2018-04-05T12:30:15Z" 1509 
VTL Mask:    YYYY-MM-DDThh:mm:ssZ/YYYY-MM-DDThh:mm:ssZ 1510 
 Start and duration, such as "2015-03-03T09:30:45-01/P1Y2M10DT2H30M" 1511 
VTL Mask:    YYYY-MM-DDThh:mm:ss-01/PY\YM\MDD\DT{h}h\Hmm\M 1512 
 Duration and end, such as "P1Y2M10DT2H30M/2018-04-05T12:30:00+02" 1513 
VTL Mask:    PY\YM\MDD\DT{h}h\Hmm\M/YYYY-MM-DDThh:mm:ssZ 1514 
Example of other possible ISO formats having accuracy reduced to the day 1515 
 Start and end, such as "20150303/20180405" 1516 
VTL Mask:    YYYY-MM-DD/YYYY-MM-DD 1517 
 Start and duration, such as "2015-03-03/P1Y2M10D" 1518 
VTL Mask:    YYYY-MM-DD/PY\YM\MDD\D 1519 
 Duration and end, such as "P1Y2M10D/2018-04-05" 1520 
VTL Mask:    PY\YM\MDD\DT/YYYY-MM-DD 1521 
 1522 
Examples of formatting masks for the date scalar type: 1523 
A date scalar type is a point in time, equivalent to an interval of time having coincident start and end duration 1524 
equal to zero.  1525 
These examples about possible ISO 8601 formats for expressing dates: 1526 
 Date and day time with separators:  "2015-03-03T09:30:45Z" 1527 
VTL Mask:    YYYY-MM-DDThh:mm:ssZ 1528 
 Date and day time without separators  "20150303T093045-01 " 1529 
VTL Mask:    YYYYMMDDThhmmss-01 1530 
Example of other possible ISO formats having accuracy reduced to the day 1531 
 Date and day-time with separators "2015-03-03/2018-04-05" 1532 
VTL Mask:    YYYY-MM-DD/YYYY-MM-DD 1533 
 Start and duration, such as "2015-03-03/P1Y2M10D" 1534 
VTL Mask:    YYYY-MM-DD/PY\YM\MDD\D 1535 
 1536 
Examples of formatting masks for the time_period scalar type: 1537 
A time_period denotes non-overlapping time intervals having a regular duration  (for example the years, the 1538 
quarters of years, the months, the weeks and so on). The time_period values include the representation of the 1539 
duration of the period. 1540 
These examples are about possible formats for expressing time-periods: 1541 
 Generic time period within the year such as:  "2015Q4", "2015M12""2015D365" 1542 
VTL Mask:    YYYYP{ppp} where P is the period indicator and ppp three digits for the number of 1543 
periods, in the values, the period indicator may assume one of the values of the duration scalar type 1544 
listed below. 1545 
 Monthly period:  "2015M03" 1546 
VTL Mask:    YYYY\MMM 1547 
 1548 
51 
 
Examples of formatting masks for the duration scalar type: 1549 
A Scalar Value of type duration denotes the length of a time interval expressed with any precision and without 1550 
connection to any particular time point (for example one year, half month, one hour and fifteen minutes). 1551 
These examples are about possible formats for expressing durations (period / frequency) 1552 
 Non ISO representation of the duration in one character, whose possible codes are: 1553 
Code  Duration 1554 
  D  Day 1555 
  W  Week 1556 
  M  Month 1557 
  Q  Quarter  1558 
  S  Semester 1559 
  A  Year 1560 
VTL Mask: P (period indicator) 1561 
 ISO 8601 composite duration:   "P10Y2M12DT02H30M15S"  (P stands for “period”) 1562 
VTL Mask:    \PYY\YM\MDD\DThh\Hmm\Mss\S 1563 
 ISO 8601 duration in weeks:   "P018W"   (P stands for “period”) 1564 
VTL Mask:    \PWWW\W 1565 
 ISO 4 characters representation:   P10M (ten months), P02Q (two quarters) … 1566 
VTL Mask:   \PppP 1567 
 1568 
Examples of fixed characters used in the ISO 8601 standard which can appear as fixed characters in the relevant 1569 
masks: 1570 
P designator of duration 1571 
T designator of time 1572 
Z designator of UTC zone 1573 
“+” designator of offset from UTC zone 1574 
”-“           designator of offset form UTC zone 1575 
/ time interval separator 1576 
 1577 
Attribute propagation  1578 
The VTL has different default behaviours for Attributes and for Measures, to comply as much as possible with the 1579 
relevant manipulation needs. At the Data Set level, the VTL Operators manipulate by default only the Measures 1580 
and not the Attributes. At the Component level, instead, Attributes are calculated like Measures, therefore the 1581 
algorithms for calculating Attributes, if any, can be specified explicitly in the invocation of the Operators.  This is 1582 
the behaviour of clauses like calc, keep, drop, rename and so on, either inside or outside the join (see the 1583 
detailed description of these operators in the Reference Manual).  1584 
The users which want to automatize the propagation of the Attributes’ Values can optionally enforce a 1585 
mechanism, called Attribute Propagation rule, whose behaviour is explained in the User Manual (see the section 1586 
“Behaviour for Attribute Components”). The adoption of this mechanism is optional, users are free to allow the 1587 
attribute propagation rule or not. The users that do not want to allow Attribute propagation rules simply will not 1588 
implement what follows. 1589 
In short, the automatic propagation of an Attribute depends on a Boolean characteristic, called “virality”, which 1590 
can be assigned to any Attribute of a Data Set (a viral Attribute has virality = TRUE, a non-viral Attribute has 1591 
virality=FALSE, if the virality is not defined, the Attribute is considered as non-viral).   1592 
By default, an Attribute propagates from the operand Data Sets (DS_i) to the result Data Set (DS_r) if it is “viral” 1593 
at least in one of the operand Data Sets. By default, an Attribute which is viral in one of the operands DS_i is 1594 
considered as viral also in the result DS_r.  1595 
52 
 
The Attribute propagation rule does not apply for the time series operators. 1596 
The Attribute propagation rule does not apply if the operations on the Attributes to be propagated are explicitly 1597 
specified in the expression (for example through the keep and calc operators). This way it is possible to keep in 1598 
the result also Attribute which are non-viral in all the operands, to drop viral Attributes, to override the 1599 
(possible) default calculation algorithm of the Attribute, to change the virality of the resulting Attributes.    1600 
 1601 
 1602 
 1603 
53 
 
VTL-ML  -  General purpose operators  1604 
Parentheses :   ( ) 1605 
 1606 
Syntax 1607 
( op ) 1608 
 1609 
Input parameters 1610 
op   the operand to be evaluated before performing other operations written outside the parentheses.  1611 
According to the general VTL rule, operators can be nested, therefore any Data Set, Component or scalar 1612 
op can be obtained through an expression as complex as needed (for example op can be written as the 1613 
expression  2 + 3 ). 1614 
 1615 
Examples of valid syntaxes 1616 
( DS_1  +  DS_2 ) 1617 
( CMP_1  -  CMP_2 ) 1618 
( 2  +  DS_1 ) 1619 
( DS_2   -   3   *  DS_3 ) 1620 
 1621 
Semantic for scalar operations 1622 
Parentheses override the default evaluation order of the operators that are described in the section “VTL-ML – 1623 
Evaluation order of the Operators”. The operations enclosed in the parentheses are evaluated first. For example 1624 
(2+3)*4 returns 20, instead 2+3*4 returns 14 because the multiplication has higher precedence than the 1625 
addition. 1626 
 1627 
Input parameters type 1628 
op ::      dataset  1629 
  |   component  1630 
|   scalar       1631 
 1632 
Result type 1633 
result ::   dataset   1634 
|   component  1635 
|   scalar       1636 
 1637 
Additional constraints 1638 
None. 1639 
 1640 
Behaviour 1641 
As mentioned, the op of the parentheses can be obtained through an expression as complex as needed (for 1642 
example op can be written as  DS_1 - DS_2. The part of the expression inside the parentheses is evaluated 1643 
before the part outside of the parentheses. If more parentheses are nested, the inner parentheses are evaluated 1644 
first, for example   ( 20 – 10 / (2 + 3) ) * 3  would give  54.  1645 
 1646 
Examples 1647 
(DS_1 + DS_2) * DS_3 1648 
(CMP_1 – CMP_2 / (CMP_3 + CMP_4) ) * CMP_5 1649 
Persistent assignment :   <- 1650 
 1651 
Syntax   1652 
re <-  op 1653 
 1654 
54 
 
Input Parameters 1655 
re the result 1656 
op the operand. According to the general VTL rule allowing the indentation of the operators, op can be 1657 
obtained through an expression as complex as needed (for example op can be the expression DS_1  -  1658 
DS_2). 1659 
 1660 
Examples of valid syntaxes   1661 
DS_r   <-   DS_1 1662 
DS_r   <-   DS_1  -  DS_2 1663 
 1664 
Semantics for scalar operations 1665 
empty 1666 
 1667 
Input parameters type  1668 
 op ::  dataset    1669 
   1670 
 1671 
Result type 1672 
result ::       dataset    1673 
 1674 
Additional constraints 1675 
The assignment cannot be used at Component level because the result of a Transformation cannot be a Data Set 1676 
Component. When operations at Component level are invoked, the result is the Data Set which the output 1677 
Components belongs to.  1678 
 1679 
Behaviour 1680 
The input operand op is assigned to the persistent result re, which assumes the same value as op. As mentioned, 1681 
the operand op can be obtained through an expression as complex as needed (for example op can be the 1682 
expression DS_1 -  DS_2).  1683 
The result re is a persistent Data Set that has the same data structure as the Operand.  For example in DS_r <- 1684 
DS_1 the data structure of DS_r is the same as the one of DS_1. 1685 
If the Operand op is a scalar value, the result Data Set has no Components and contains only such a scalar value. 1686 
For example, income <-  3  assigns the value 3 to the persistent Data Set named  income.    1687 
 1688 
Examples  1689 
 1690 
Given the operand Data Set DS_1: 1691 
 1692 
DS_1 
Id_1 Id_2 Me_1 Me_2 
2013 Belgium 5 5 
2013 Denmark 2 10 
2013 France 3 12 
2013 Spain 4 20 
 1693 
Example 1:  DS_r   <-   DS_1 results in: 1694 
 1695 
DS_r  (persistent Data  Set) 
Id_1 Id_2 Me_1 Me_2 
2013 Belgium 5 5 
2013 Denmark 2 10 
2013 France 3 12 
2013 Spain 4 20 
55 
 
Non-persistent assignment :   :=     1696 
Syntax   1697 
re :=  op 1698 
 1699 
Input parameters 1700 
re the result 1701 
op the operand (according to the general VTL rule allowing the indentation of the operators, op can be 1702 
obtained through an expression as complex as needed (for example op can be the expression  DS_1  -  1703 
DS_2). 1704 
 1705 
Examples of valid syntaxes 1706 
DS_r     :=    DS_1 1707 
DS_r     :=    3 1708 
DS_r     :=    DS_1 -  DS_2 1709 
DS_r     :=    3 + 2 1710 
 1711 
Semantic for scalar operations 1712 
empty 1713 
 1714 
Input parameters type 1715 
 op ::      dataset 1716 
  |  scalar 1717 
 1718 
Result type 1719 
result ::       dataset 1720 
 1721 
Additional constraints 1722 
The assignment cannot be used at Component level because the result of a Transformation cannot be a Data Set 1723 
Component. When operations at Component level are invoked, the result is the Data Set which the output 1724 
Components belongs to.  1725 
The same symbol denoting the non-persistent assignment Operator (:=) is also used inside other operations at 1726 
Component level (for example in calc and aggr) in order to assign the result of the operation to the output 1727 
Component: please note that in these cases the symbol := does not denote the non-persistent assignment (i.e., 1728 
this Operator), which cannot operate at Component level, but a special keyword of the syntax of the other 1729 
Operator in which it is used.  1730 
 1731 
Behaviour 1732 
The value of the operand op is assigned to the result re, which is non-persistent and therefore is not stored. As 1733 
mentioned, the operand op can be obtained through an expression as complex as needed (for example op can be 1734 
the expression DS_1  -  DS_2).  1735 
The result re is a non-persistent Data Set that has the same data structure as the Operand.  For example in DS_r 1736 
:= DS_1 the data structure of DS_r is the same as the one of DS_1. 1737 
If the Operand op is a scalar value, the result Data Set has no Components and contains only such a scalar value. 1738 
For example, income :=  3  assigns the value 3 to the non-persistent Data Set named  income.    1739 
 1740 
Examples  1741 
 1742 
Given the operand Data Sets DS_1: 1743 
 1744 
DS_1 
Id_1 Id_2 Me_1 Me_2 
2013 Belgium 5 5 
2013 Denmark 2 10 
2013 France 3 12 
2013 Spain 4 20 
 1745 
56 
 
Example 1:  DS_r  :=  DS_1  results in: 1746 
 1747 
DS_r  (non persistent Data Set) 
Id_1 Id_2 Me_1 Me_2 
2013 Belgium 5 5 
2013 Denmark 2 10 
2013 France 3 12 
2013 Spain 4 20 
 1748 
Membership :      # 1749 
 1750 
Syntax   1751 
ds#comp 1752 
 1753 
Input Parameters 1754 
ds  the Data Set 1755 
comp  the Data Set Component 1756 
 1757 
Examples of valid syntaxes   1758 
DS_1#COMP_3 1759 
 1760 
Semantic for scalar operations 1761 
This operator cannot be applied to scalar values. 1762 
 1763 
Input parameters type 1764 
ds ::  dataset  1765 
comp ::  name < component > 1766 
 1767 
Result type 1768 
result ::       dataset  1769 
 1770 
Additional constraints 1771 
comp must be a Data Set Component of the Data Set ds 1772 
 1773 
Behaviour 1774 
The membership operator returns a Data Set having the same Identifier Components of ds and a single Measure.  1775 
If comp is a Measure in ds, then comp is maintained in the result while all other Measures are dropped.  1776 
If comp is an Identifier or an Attribute Component in ds, then all the existing Measures of ds are dropped in the 1777 
result and a new Measure is added. The Data Points’ values for the new Measure are the same as the values of 1778 
comp in ds. A default conventional name is assigned to the new Measure depending on its type: for example 1779 
num_var if the Measure is numeric, string_var if it is string and so on (the default name can be renamed through 1780 
the rename operator if needed).  1781 
The Attributes follow the Attribute propagation rule as usual (viral Attributes of ds are maintained in the result 1782 
as viral, non-viral ones are dropped). If comp is an Attribute, it follows the Attribute propagation rule too. 1783 
The same symbol denoting the membership operator (#) is also used inside other operations at Component level 1784 
(for example in join, calc, aggr) in order to identify the Components to be operated: please note that in these 1785 
cases the symbol # does not denote the membership operator (i.e., this operator, which does not operate at 1786 
Component level), but a special keyword of the syntax of the other operator in which it is used.  1787 
 1788 
 1789 
Examples  1790 
Given the operand Data Set DS_1: 1791 
 1792 
57 
 
DS_1 
Id_1 Id_2 Me_1 Me_2 At_1 
1 A 1 5  
1 B 2 10 P 
2 A 3 12  
 1793 
Example 1:  DS_r  := DS_1#Me_1  results in: 1794 
 1795 
(assuming that At_1 is not viral in DS_1) 1796 
 1797 
DS_r 
Id_1 Id_2 Me_1 
1 A 1 
1 B 2 
2 A 3 
 1798 
(assuming that At_1 is viral in DS_1) 1799 
 1800 
DS_r 
Id_1 Id_2 Me_1 At_1 
1 A 1  
1 B 2 P 
2 A 3  
 1801 
Example 2: DS_r  := DS_1#Id_1  assuming that At_1 is viral in DS_1 results in: 1802 
 1803 
DS_r 
Id_1 Id_2 num_var At_1 
1 A 1  
1 B 1 P 
2 A 2  
 1804 
Example 3: DS_r  := DS_1#At_1  assuming that At_1 is viral in DS_1 results in: 1805 
 1806 
DS_r 
Id_1 Id_2 string_var At_1 
1 A   
1 B P P 
2 A   
 1807 
User-defined operator call 1808 
 1809 
Syntax   1810 
operatorName ( { argument { , argument }* } ) 1811 
 1812 
58 
 
Input parameters 1813 
operatorName   the name of an existing user-defined operator  1814 
argument   argument passed to the operator 1815 
 1816 
Examples of valid syntaxes 1817 
max1 ( 2, 3 ) 1818 
 1819 
Semantic for scalar operations 1820 
It depends on the specific user-defined operator that is invoked. 1821 
 1822 
Input parameters type 1823 
operatorName :: name 1824 
argument :: A data type compatible with the type of the parameter of the user-defined operator that 1825 
is invoked  (see also the “Type syntax” section). 1826 
 1827 
 1828 
Result type 1829 
result ::    The data type of the result of the user-defined operator that is invoked (see also the 1830 
“Type syntax” section). 1831 
 1832 
Additional constraints 1833 
 operatorName must refer to an operator created with the define operator statement.  1834 
 The type of each argument value must be compliant with the type of the corresponding parameter of the 1835 
user defined operator (the correspondence is in the positional order). 1836 
 1837 
Behaviour 1838 
The invoked user-defined operator is evaluated. The arguments passed to the operator in the invocation are 1839 
associated to the corresponding parameters in positional order, the first argument as the value of the first 1840 
parameter, the second argument as the value of the second parameter, and so on.  An underscore (“_”) can be 1841 
used to denote that the value for an optional operand is omitted. One or more optional operands in the last 1842 
positions can be simply omitted.  1843 
 1844 
Examples 1845 
Example 1:  1846 
 1847 
Definition of the max1 operator (see also “define operator” in the VTL-DL): 1848 
 1849 
define operator max1 (x integer, y integer) 1850 
returns boolean  1851 
is   if x > y then x else y 1852 
end define operator 1853 
 1854 
User-defined operator call of the max1 operator: 1855 
 1856 
max1 ( 2, 3 ) 1857 
 1858 
Evaluation of an external routine :  eval 1859 
 1860 
Syntax 1861 
eval   (  externalRoutineName ( { argument }  { , argument }* ), language,  returns  outputType ) 1862 
 1863 
Input parameters 1864 
externalRoutineName  the name of an external routine  1865 
argument the arguments passed to the external routine  1866 
language the implementation language of the routine 1867 
outputType   the data type of the object returned by eval (see the section: Data type syntax) 1868 
 1869 
59 
 
Examples of valid syntaxes 1870 
eval ( routine1 ( DS_1 ) ) 1871 
 1872 
Semantics for scalar operations: 1873 
This is not a scalar operation. 1874 
 1875 
Input parameters type 1876 
externalRoutineName ::  name  1877 
argument ::    any data type 1878 
language ::   string 1879 
outputType ::   any data type restricting Data Set or scalar 1880 
 1881 
Result Type 1882 
result ::     dataset 1883 
  1884 
Additional constraints 1885 
 The eval is the only VTL Operator that does not allow nesting and therefore a Transformation can contain 1886 
just one invocation of eval and no other invocations. In other words, eval cannot be nested as  the operand 1887 
of another operation as well as another operator cannot be nested as an operand of eval 1888 
 The result of an expression containing eval must be persistent 1889 
 externalRoutineName is the conventional name of a non-VTL routine  1890 
 the invoked external routine must be consistent with the VTL principles, first of all its behaviour must be 1891 
functional, so having in input and providing in output first-order functions  1892 
 argument  is an argument passed to the external routine, it can be a name or a value of a VTL artefacts or 1893 
some other parameter required by the routine 1894 
 the arguments passed to the routine correspond to the parameters of the invoked external routine in 1895 
positional order; as usual the optional parameters are substituted by the underscore if missing. The 1896 
conversion of the VTL input/output data types from and to the external routine processor is left to the 1897 
implementation.  1898 
 1899 
Behaviour 1900 
The eval operator invokes an external, non-VTL routine, and returns its result as a Data Set or a scalar. The 1901 
specific data type can be given in the invocation. The routine specified in the eval operator can perform any 1902 
internal logic. 1903 
 1904 
Examples 1905 
Assuming that SQL3 is an SQL statement which produces DS_r starting from DS_1: 1906 
 1907 
DS_r := eval( SQL3( DS_1 ) , “SQL”, 1908 
returns dataset { identifier<geo_area> ref_area,  1909 
identifier<date> time,  1910 
measure<number> obs_value,  1911 
attribute<string> obs_status }  ) 1912 
 1913 
Assuming that f is an externally defined Java method: 1914 
 1915 
DS_r := DS_1[calc Me := eval( f(Me) + 1, “Java”, integer) ] 1916 
 1917 
Type conversion :  cast 1918 
Syntax   1919 
cast ( op , scalarType { , mask} ) 1920 
 1921 
Input parameters 1922 
op    the operand to be cast 1923 
scalarType  the name of the scalar type into which op has to be converted 1924 
mask  a character literal that specifies the format of op 1925 
 1926 
60 
 
Examples of valid syntaxes  1927 
See the examples below. 1928 
 1929 
Semantics for scalar operations: 1930 
This operator converts the scalar type of op to the scalar type specified by scalarType.  It returns a copy of op 1931 
converted to the specified scalarType. 1932 
 1933 
Input parameters type 1934 
op ::   dataset{ measure<scalar> _ } 1935 
  | component<scalar> 1936 
  | scalar 1937 
scalarType ::  scalar type    (see the section: Data type syntax) 1938 
mask ::   string 1939 
 1940 
Result type 1941 
result ::  dataset{ measure<scalar> _ } 1942 
  | component<scalar> 1943 
  | scalar 1944 
  1945 
Additional constraints 1946 
 Not all the conversions are possible, the specified casting operation is allowed only according to the 1947 
semantics described below. 1948 
 The mask must adhere to one of the formats specified below. 1949 
 1950 
Behaviour 1951 
Conversions between basic scalar types 1952 
The VTL assumes that a basic scalar type has a unique internal and more possible external representations 1953 
(formats).  1954 
The external representations are those of the Value Domains which refers to such a basic scalar types (more 1955 
Value Domains can refer to the same basic scalar type, see the VTL Data Types in the User Manual). For example, 1956 
there can exist a boolean Value Domain which uses the values TRUE and FALSE and another boolean Value 1957 
Domain which uses the values 1 and 0. The external representations are the ones of the Data Point Values and 1958 
are obviously known by users. 1959 
The unique internal representation of a basic scalar type, instead, is used by the cast operator as a technical 1960 
expedient to make the conversion between external representations easier: not necessarily users are aware of it. 1961 
In a conversion, the cast converts the source external representation into the internal representation (of the 1962 
corresponding scalar type), then this last one is converted into the target external representation (of the target 1963 
type). As mentioned in the User Manual, VTL does not prescribe any specific internal representation for the 1964 
various scalar types, leaving different organisations free of using their preferred or already existing ones.  1965 
In some cases, depending on the type of op, the output scalarType and the invoked operator, an automatic 1966 
conversion is made, that is, even without the explicit invocation of the cast operator: this kind of conversion is 1967 
called implicit casting.  1968 
In other cases, more than all when the implicit casting is not possible, the type conversion must be specified 1969 
explicitly through the invocation of the cast operator: this kind of conversion is called explicit casting.  If an 1970 
explicit casting is specified, the (possible) implicit casting is overridden. There are two main categories of 1971 
implicit casting: 1972 
 “Explicit with mask”: the explicit conversion requires a formatting mask that specifies how the actual 1973 
casting is performed; 1974 
 “Explicit w/o mask”: the explicit conversion does not requires a formatting mask. 1975 
The table below summarises the possible castings between the basic scalar types. In particular, the input type is 1976 
specified in the first column (row headings) and the output type in the first row (column headings).  1977 
 1978 
Expected 
 
Provided               
integer number boolean time date time_period string duration 
integer - Implicit Explicit w/o 
mask 
Not feasible Not feasible Not feasible Implicit Not 
feasible 
61 
 
number Explicit w/o 
mask - Explicit w/o 
mask 
Not feasible Not feasible Not feasible Implicit Not 
feasible 
boolean Explicit w/o 
mask 
Explicit w/o 
mask - Not feasible Not feasible Not feasible Implicit Not 
feasible 
time Not feasible Not feasible Not feasible - Not feasible Not feasible Explicit with 
mask 
Not 
feasible 
date Not feasible Not feasible Not feasible Implicit - Explicit w/o 
mask 
Explicit with 
mask 
Not 
feasible 
time_period Not feasible Not feasible Not feasible Implicit Explicit with 
mask - Explicit w/o 
mask 
Not 
feasible 
string Explicit w/o 
mask 
Explicit with 
mask 
Not feasible Explicit with 
mask 
Explicit with 
mask 
Explicit with 
mask - Explicit 
with mask 
duration Not feasible Not feasible Not feasible Not feasible Not feasible Not feasible Explicit with 
mask - 
 1979 
The type of casting can be personalised in specific environments, provided that the personalisation is explicitly 1980 
documented with reference to the table above. For example, assuming that an explicit cast with mask is 1981 
required and that in a specific environment a definite mask is used for such a kind of conversions, the cast can 1982 
also become implicit provided that the mask that will be applied is specified. 1983 
The implicit casting is performed when a value of a certain type is provided when another type is expected. Its 1984 
behaviour is described here: 1985 
 From integer to number: an integer is provided when a number is expected (for example, an integer and a 1986 
number are passed as inputs of a n-ary numeric operator); it returns a number having the integer part equal 1987 
to the integer and the decimal part equal to zero; 1988 
 From integer to string:  an integer is provided when a string is expected (for example, an integer is passed 1989 
as an input of a string operator); it returns a string having the literal value of the integer; 1990 
 From number to string: a number is provided when a string is expected; it returns the string having the 1991 
literal value of the number; the decimal separator is converted into the character “.” (dot). 1992 
 From boolean to string: a boolean is provided when a string is expected; the boolean value TRUE is 1993 
converted into the string “TRUE” and  FALSE into the string “FALSE”; 1994 
 From date to time: a date (point in time) is provided when a time is expected (interval of time): the 1995 
conversion results in an interval having the same start and end, both equal to the original date; 1996 
 From time_period to time: a time_period (a regular interval of time, like a month, a quarter, a year …) is 1997 
provided when a time (any interval of time) is expected; it returns a time value having the same start and 1998 
end as the time_period value.   1999 
An implicit cast is also performed from a value domain type or a set type to a basic scalar type: when a scalar 2000 
value belonging to a Value Domains or a Set is involved in an operation (i.e., provided as input to an operator), 2001 
the value is implicitly cast into the basic scalar type which the Value Domain refers to (for this relationship, see 2002 
the description of Type System in the User Manual). For example, assuming that the Component birth_country is 2003 
defined on the Value Domain country, which contains the ISO 3166-1 numeric codes and therefore refers to the 2004 
basic scalar type integer, the (possible) invocation length(birth_country), which calculates the length of the input 2005 
string, automatically casts the values of birth_country into the corresponding string. If the basic scalar type of the 2006 
Value Domain is not compatible with the expression where it is used, an error is raised. This VTL feature is 2007 
particularly important as it provides a general behaviour for the Value Domains and relevant Sets, preventing 2008 
from the need of defining specific behaviours (or methods or operations) for each one of them. In other words, 2009 
all the Values inherit the operations that can be performed on them from the basic scalar types of the respective 2010 
Value Domains. 2011 
The cast operator can be invoked explicitly even for the conversions which allow an implicit cast and in this case 2012 
the same behaviour as the implicit cast is applied. 2013 
The behaviour of the cast operator for the conversions that require explicit casting without mask is the 2014 
following: 2015 
 From integer to boolean: if the integer is different from 0, then TRUE is returned, FALSE otherwise. 2016 
 From number to integer: converts a number with no decimal part into an integer; if the decimal part is 2017 
present, a runtime error is raised.  2018 
 From number to boolean: if the number is different from 0.0, then TRUE is returned, FALSE otherwise. 2019 
62 
 
 From boolean to integer: TRUE is converted into 1; FALSE into 0. 2020 
 From boolean to number: TRUE is converted into 1.0; FALSE into 0.0. 2021 
 From date to time_period: it converts a date into the corresponding daily value of time_period.  2022 
 From string to integer: the integer having the literal value of the string is returned; if the string contains a 2023 
literal that cannot be matched to an integer, a runtime error is raised. 2024 
 From string to time_period: it converts a string value to a time_period value.  2025 
When an explicit casting with mask is required, the conversion is made by applying the formatting mask which 2026 
specifies the meaning of the characters in the output string. The formatting Masks are described in the section 2027 
“VTL-ML – Typical Behaviour of the ML Operators”, sub-section “Type Conversion and Formatting Mask.  2028 
The behaviour of the cast operator for such conversions is the following: 2029 
 From time to string: it is applied the time formatting mask.  2030 
 From date to string: it is applied the time_period formatting mask.  2031 
 From time_period to date: it is applied a formatting mask which accepts two possible values (“START”, 2032 
“END”). If “START” is specified, then the date is set to the beginning of the time_period; if “END” is specified, 2033 
then the date is set to the end of the time_period. 2034 
 From time_period to string:  it is applied the time_period formatting mask. 2035 
 From duration to string: a duration (an absolute time interval) is provided when a string is expected; it 2036 
returns the string having the default string representation for the duration. 2037 
 From string to number: the number having the literal value of the string is returned; if the string contains a 2038 
literal that cannot be matched to a number, a runtime error is raised. The number is generated by using a 2039 
number formatting mask.  2040 
 From string to time: the time having the literal value of the string is returned; if the string contains a literal 2041 
that cannot be matched to a date, a runtime error is raised. The time value is generated by using a time 2042 
formatting mask. 2043 
 From string to duration: the duration having the literal value of the string is returned; if the string contains 2044 
a literal that cannot be matched to a duration, a runtime error is raised. The duration value is generated by 2045 
using a time formatting mask. 2046 
Conversions between basic scalar types and Value Domains or Set types 2047 
A value of a basic scalar type can be converted into a value belonging to a Value Domain which refers to such a 2048 
scalar type. The resulting scalar value must be one of the allowed values of the Value Domain or Set; otherwise, a 2049 
runtime error is raised. This specific use of cast operators does not really correspond to a type conversion; in 2050 
more formal terms, we would say that it acts as a constructor, i.e., it builds an instance of the output type. Yet, 2051 
towards a homogeneous and possibly simple definition of VTL syntax, we blur the distinction between 2052 
constructors and type conversions and opt for a unique formalism. An example is given below. 2053 
Conversions between different Value Domain types 2054 
As a result of the above definitions, conversions between values of different Value Domains are also possible. 2055 
Since an element of a Value Domain is implicitly cast into its corresponding basic scalar type, we can build on it 2056 
to turn the so obtained scalar type into another Value Domain type. Of course, this latter Value Domain type must 2057 
use as a base type this scalar type. 2058 
 2059 
Examples 2060 
 2061 
Example 1: from string to number 2062 
ds2 := ds1[calc m2 := cast(m1, number, “DD.DDD”) + 2) ] 2063 
In this case we use explicit cast from string to numbers. The mask is used to specify how the string must be 2064 
interpreted in the conversion. 2065 
 2066 
Example 2: from string to date 2067 
ds2 := ds1[calc m2 := cast(m1, date, “YYYY-MM-DD”) ] 2068 
In this case we use explicit cast from string to date. The mask is used to specify how the string must be 2069 
interpreted in the conversion. 2070 
 2071 
63 
 
Example 3: from number to integer 2072 
ds2 := ds1[calc m2 := cast(m1, integer) + 3 ] 2073 
In this case we cast a number into an integer, no mask is required. 2074 
 2075 
Example 4: from number to string 2076 
ds2 := ds1[calc m2 := length(cast(m1, string)) ] 2077 
In this case we cast a number into a string, no mask is required. 2078 
 2079 
Example 5: from date to string 2080 
ds2 := ds1[calc m2 := cast(m1, string, “YY-MON-DAY hh:mm:ss”) ] 2081 
In this example a date instant is turned into a string. The mask is used to specify the string layout. 2082 
 2083 
Example 6: from string to GEO_AREA 2084 
ds2 := ds1[calc m2 := cast(GEO_STRING, GEO_AREA)] 2085 
In this example we suppose we have elements of Value Domain Subset for GEO_AREA. Let GEO_STRING be a 2086 
string Component of Data Set ds1 with string values compatible with the GEO_AREA Value Domain Subset. 2087 
Thus, the following expression moves ds1 data into ds2, explicitly casting strings to geographical areas.  2088 
 2089 
Example 7: from GEO_AREA to string 2090 
ds2 := ds1[calc m2 := length(GEO_AREA)] 2091 
In this example we use a Component GEO_AREA in a string expression, which calculates the length of the 2092 
corresponding string; this triggers the automatic cast. 2093 
 2094 
Example 8: from GEO_AREA2 to GEO_AREA1 2095 
ds2 := ds1 [ calc m2 := cast (GEO, GEO_AREA1) ] 2096 
In this example we suppose we have to compare elements two Value Domain Subsets, They are both defined on 2097 
top of Strings. The following cast expressions performs the conversion. 2098 
Now, Component GEO is of type GEO_AREA2, then we specify it has to be cast into GEO_AREA1. As both 2099 
work on strings (and the values are compatible), the conversion is feasible. In other words, the cast of an 2100 
operand into GEO_AREA1 would expect a string. Then, as GEO is of type GEO_AREA2, defined on top of 2101 
strings, it is implicitly cast to the respective string; this is compatible with what cast expects and it is then able to 2102 
build a value of type GEO_AREA1. 2103 
 2104 
Example 9: from string to time_period 2105 
In the following examples we convert from strings to time_periods, by using appropriate masks. 2106 
The first quarter of year 2000 can be expressed as follows (other examples are possible): 2107 
cast ( “2000Q1”, time_period, “YYYY\QQ” ) 2108 
cast ( “2000-Q1”, time_period, “YYYY-\QQ” ) 2109 
cast ( “2000-1”, time_period, “YYYY-Q” ) 2110 
cast ( “Q1-2000”, time_period, “\QQ-YYYY” ) 2111 
cast ( “2000Q01”, time_period, “YYYY\QQQ” ) 2112 
Examples of daily data: 2113 
cast ( “2000M01D01”, time_period, “YYYY\MMM\DDD” ) 2114 
cast ( “2000.01.01”, time_period, “YYYY\.MM\.DD” ) 2115 
 2116 
64 
 
VTL-ML  -  Join operators 2117 
The Join operators are fundamental VTL operators. They are part of the core of the language and allow to obtain 2118 
the behaviour of the majority of the other non-core operators, plus many additional behaviours that cannot be 2119 
obtained through the other operators. 2120 
The Join operators are four, namely the inner_join, the left_join, the full_join and the cross_join. Because their 2121 
syntax is similar, they are described together. 2122 
Join : inner_join,  left_join,  full_join,  cross_join 2123 
Syntax   2124 
joinOperator (  ds1 { as alias1 } { , dsN { as aliasN } }* { using usingComp { , usingComp }* }  2125 
{ filter filterCondition }  2126 
{ apply applyExpr 2127 
  | calc calcClause  2128 
        | aggr aggrClause { groupingClause } }  2129 
{ keep comp {, comp }* | drop comp {, comp }* } 2130 
{ rename compFrom to compTo { , compFrom to compTo }* } 2131 
        ) 2132 
joinOperator ::=  { inner_join | left_join | full_join | cross_join }1 2133 
calcClause  ::=  { calcRole } calcComp := calcExpr    2134 
{ , { calcRole } calcComp := calcExpr }* 2135 
calcRole            ::=  {identifier | measure | attribute | viral attribute}1 2136 
aggrClause  ::=  { aggrRole } aggrComp := aggrExpr  2137 
{ , { aggrRole } aggrComp := aggrExpr }*  2138 
aggrRole           ::=  { measure | attribute | viral attribute }1 2139 
groupingClause  ::=  { group by   groupingId { , groupingId }* 2140 
| group except   groupingId { , groupingId }* 2141 
| group all conversionExpr }1 2142 
   { having havingCondition }   2143 
 2144 
 2145 
Input parameters 2146 
joinOperator  the Join operator to be applied 2147 
ds1, …, dsN  the Data Set operands (at least one must be present) 2148 
alias1, …, aliasN optional aliases for the input Data Sets, valid only within the “join” operation to make it 2149 
easier to refer to them. If omitted, the Data Set name must be used.  2150 
usingComp component of the input Data Sets whose values have to match in the join  (the using 2151 
clause is allowed for the left_join only under certain constraints described below and is 2152 
not allowed at all for the full_join and cross_join) 2153 
filterCondition a condition (boolean expression) at component level, having only Components of the 2154 
input Data Sets as operands, which is evaluated for each joined Data Point and filters 2155 
them (when TRUE the joined Data Point is kept, otherwise it is not kept)  2156 
applyExpr an expression, having the input Data Sets as operands, which is pairwise applied to all 2157 
their homonym Measure Components and produces homonym Measure Components in 2158 
the result; for example if both the Data Sets ds1 and ds2 have the numeric measures m1 2159 
and m2, the clause apply ds1 + ds2 would result in calculating m1 := ds1#m1 +  2160 
ds2#m1  and m2 := ds1#m2 +  ds2#m2   2161 
calcClause clause that specifies the Components to be calculated, their roles and their calculation 2162 
algorithms, to be applied on the joined and filtered Data Points. 2163 
calcRole the role of the Component to be calculated  2164 
calcComp  the name of the Component to be calculated  2165 
65 
 
calcExpr expression at component level, having only Components of the input Data Sets as 2166 
operands, used to calculate a Component  2167 
aggrClause clause that specifies the required aggregations, i.e., the aggregated Components to be 2168 
calculated, their roles and their calculation algorithm, to be applied on the joined and 2169 
filtered Data Points 2170 
aggrRole the role of the aggregated Component to be calculated; if omitted, the Measure role is 2171 
assumed 2172 
aggrComp the name of the aggregated Component to be calculated; this is a dependent Component 2173 
of the result (Measure or Attribute, not Identifier) 2174 
aggrExpr expression at component level, having only Components of the input Data Sets as 2175 
operands, which invokes an aggregate operator (e.g.  avg, count, max … , see also the 2176 
corresponding sections) to perform the desired aggregation. Note that the count 2177 
operator is used in an aggrClause without parameters, e.g.:  2178 
DS_1 [ aggr Me_1 := count ( ) group by Id_1 ) ] 2179 
groupingClause the following alternative grouping options: 2180 
group by the Data Points are grouped by the values of the specified Identifiers 2181 
(groupingId). The Identifiers not specified are dropped in the result. 2182 
group except the Data Points are grouped by the values of the Identifiers not 2183 
specified as groupingId. The specified Identifiers are dropped in the 2184 
result. 2185 
group all converts the values of an Identifier Component using conversionExpr 2186 
and keeps all the resulting Identifiers. 2187 
groupingId Identifier Component to be kept (in the group by clause) or dropped (in the group 2188 
except clause). 2189 
conversionExpr specifies a conversion operator (e.g. time_agg) to convert an Identifier from finer to 2190 
coarser granularity. The conversion operator is applied on an Identifier of the operand 2191 
Data Set op. 2192 
havingCondition a condition (boolean expression) at component level, having only Components of the 2193 
input Data Sets as operands (and possibly constants), to be fulfilled by the groups of 2194 
Data Points:  only groups for which havingCondition evaluates to TRUE appear in the 2195 
result. The havingCondition refers to the groups specified through the groupingClause, 2196 
therefore it must invoke aggregate operators (e.g.  avg, count, max, …, see also the 2197 
section Aggregate invocation). A correct example of havingCondition is  2198 
max(obs_value) < 1000, while the condition obs_value < 1000 is not a right 2199 
havingCondition, because it refers to the values of single Data Points and not to the 2200 
groups. The count operator is used in a havingCondition without parameters, e.g.:  2201 
sum ( ds group by id1 having count ( ) >= 10 ) 2202 
comp dependent Component (Measure or Attribute, not Identifier) to be kept (in the keep 2203 
clause) or dropped (in the drop clause)  2204 
compFrom  the original name of the Component to be renamed 2205 
compTo  the new name of the Component atfer the renaming 2206 
  2207 
Examples of valid syntaxes  2208 
inner_join  ( ds1 as d1,  ds2 as d2 using Id1, Id2 2209 
filter d1#Me1 + d2#Me1 <10 2210 
apply  d1 / d2 2211 
keep Me1, Me2, Me3  2212 
rename Id1 to Id10, id2 to id20 2213 
                   ) 2214 
 2215 
left_join ( ds1 as d1,  ds2 as d2 2216 
   filter d1#Me1 + d2#Me1 <10,  2217 
   calc Me1 := d1#Me1 + d2#Me3, 2218 
   keep  Me1  2219 
   rename Id1 to Ident1, Me1 to Meas1 2220 
  ) 2221 
 2222 
full_join ( ds1 as d1,  ds2 as d2 2223 
   filter d1#Me1 + d2#Me1 <10,  2224 
66 
 
   aggr Me1 := sum(Me1), attribute At20 := avg(Me2) 2225 
   group by  Id1, Id2  2226 
having sum(Me3) > 0  2227 
) 2228 
 2229 
Semantics for scalar operations 2230 
The join operator does not perform scalar operations. 2231 
 2232 
Input parameters type  2233 
ds1, …, dsN ::   dataset 2234 
alias1, …, aliasN :: name 2235 
usingId ::   name < component > 2236 
filterCondition ::  component<boolean> 2237 
applyExpr  ::  dataset 2238 
calcComp ::   name < component > 2239 
calcExpr ::   component<scalar> 2240 
aggrComp ::   name < component > 2241 
aggrExpr ::   component<scalar> 2242 
groupingId ::  name < identifier > 2243 
conversionExpr ::  component<scalar> 2244 
havingCondition :: component<boolean> 2245 
comp ::    name < component > 2246 
compFrom ::   component<scalar> 2247 
compTo ::   component<scalar> 2248 
 2249 
Result type 2250 
result ::        dataset  2251 
 2252 
Additional constraints 2253 
The aliases must be all distinct and different from the Data Set names. Aliases are mandatory for Data Sets which 2254 
appear more than once in the Join (self-join) and for non-named Data Set obtained as result of a sub-expression. 2255 
The using clause is not allowed for the full_join and for the cross_join, because otherwise a non-functional 2256 
result could be obtained.  2257 
If the using clause is not specified (we will label this case as “Case A”), calling Id(dsi) the set of Identifier 2258 
Components of operand dsi, the following group of constraints must hold7: 2259 
 For inner_join, for each pair dsi, dsj, either Id(dsi)  Id(dsj) or Id(dsj)  Id(dsi).  In simpler words, the 2260 
Identifiers of one of the joined Data Sets must be a superset of the identifiers of all the other ones.  2261 
 For left_join and full_join, for each pair dsi, dsj,  Id(dsi) = Id(dsj). In simpler words, the joined Data Sets 2262 
must have the same Identifiers.  2263 
 For cross-join (Cartesian product), no constraints are needed. 2264 
If the using clause is specified (we will label this case as “Case B”, allowed only for the inner_join and the 2265 
left_join), all the join keys must appear as Components in all the input Data Sets. Moreover two sub-cases are 2266 
allowed: 2267 
 Sub-case B1: the constraints of the Case A are respected and the join keys are a subset of the common 2268 
Identifiers of the joined Data Sets; 2269 
 Sub-case B2:  2270 
o In case of inner_join, one Data Set acts as the reference Data Set which the others are joined to; 2271 
in case of left_join, this is the “more to the left” Data Set (i.e., ds1);  2272 
o All the input Data Sets, except the reference Data Set, have the same Identifiers [Id1, … , Idn]; 2273 
o The using clause specifies all and only the common Identifiers of the non-reference Data Sets 2274 
[Id1, … , Idn].  2275 
The join operators must fulfil also other constraints: 2276 
 apply,  calc  and aggr clauses are mutually exclusive 2277 
 keep and drop clauses are mutually exclusive 2278 
 comp can be only dependent Components (Measures and Attributes, not Identifiers) 2279 
 An Identifier not included in the group by clause (if any) cannot be included in the rename clause 2280 
                                                           
7 These constraints hold also for the full_join and the cross_join, which do not allow the using clause. 
 
67 
 
 An Identifier included in the group except clause (if any) cannot be included in the rename clause. If the 2281 
aggr clause is invoked and the grouping clause is omitted, no Identifier can be included in the rename 2282 
clause 2283 
 A dependent Component not included in the keep clause (if any) cannot be renamed  2284 
 A dependent Component included in the drop clause (if any) cannot be renamed  2285 
 2286 
Behaviour 2287 
The semantics of the join operators can be procedurally described as follows.  2288 
 A relational join of the input operands is performed, according to SQL inner (inner_join), left-outer 2289 
(left_join), full-outer (full_join) and Cartesian product (cross_join) semantics (these semantics will be 2290 
explained below), producing an intermediate internal result, that is a Data Set that we will call “virtual” 2291 
(VDS1). 2292 
 The filterCondition, if present, is applied on VDS1, producing the Virtual Data Set VDS2. 2293 
 The specified calculation algorithms (apply, calc or aggr), if present, are applied on VDS2. For the 2294 
Attributes that have not been explicitly calculated in these clauses, the Attribute propagation rule is applied 2295 
(see the User Manual), so producing the Virtual Data Set  VDS3. 2296 
 The keep or drop clause, if present, is applied on VDS3, producing the Virtual Data Set  VDS4. 2297 
 The rename clause, if present, is applied on VDS4, producing the Virtual Data Set  VDS5.  2298 
 The final automatic alias removal is performed in order to obtain the output Data Set. 2299 
An alias can be optionally declared for each input Data Set. The aliases are valid only within the “join” operation, 2300 
in particular to allow joining a dataset with itself (self join). If omitted, the input Data Sets are referenced only 2301 
through their Data Set names. If the aliases are ambiguous (for example duplicated or equal to the name of 2302 
another Data Set), an error is raised. 2303 
The structure of the virtual Data Set  VDS1  which is the output of the relational join is the following. 2304 
For the inner_join, the left_join and the full_join, the virtual Data Set contains the following Components: 2305 
 The Components used as join keys, which appear once and maintain their original names and roles. In 2306 
the cases A and B1, all of them are Identifiers. In the sub-case B2, the result takes the roles from the 2307 
reference Data Set.  2308 
 In the sub-case B2: the Identifiers of the reference Data Set, which appear once and maintain their 2309 
original name and role. 2310 
 The other Components coming from exactly one input Data Set, which appear once and maintain their 2311 
original name 2312 
 The other Components coming from more than one input Data Set, which appears as many times as the 2313 
Data Set they come from; to distinguish them, their names are prefixed with the alias (or the name) of 2314 
the Data Set they come from, separated by the “#” symbol  (e.g.,  dsi#cmpj).  For example, if the 2315 
Component “population” appears in two input Data Sets “ds1” and “ds2” that have the  aliases “a” and 2316 
“b” respectively, the Components “a#population” and “b#population” will appear in the virtual Data Set. 2317 
If the aliases are not defined, the two Components are prefixed with the Data Set name (i.e.,  2318 
“ds1#population” and “ds2#population”). In this context, the symbol “#” does not denote the 2319 
membership operator but acts just as a separator between the the Data Set and the Component names.   2320 
 If the same Data Set appears more times as operand of the join (self-join) and the aliases are not defined, 2321 
an exception is raised because it is not allowed that two or more Components in the virtual Data Set 2322 
have the same name. In the self-join the aliases are mandatory to disambiguate the Component names. 2323 
 If a Data Set in the join list is the result of a sub-expression, then an alias is mandatory all the same 2324 
because this Data Set has no name. If the alias is omitted, an exception is raised. 2325 
As for the cross_join, the virtual Data Set contains all the Components from all the operands, possibly prefixed 2326 
with the aliases to avoid ambiguities. 2327 
The semantics of the relational join is the following. 2328 
The join is performed on some join keys, which are the Components of the input Data Sets whose values are used 2329 
to match the input Data Points and produce the joined output Data Points.  2330 
By default (only for the full_join and the cross_join), the join is performed on the subset of homonym Identifier 2331 
Components of the input Data Sets.  2332 
The parameter using allows to specify different join keys than the default ones, and can be used only for the 2333 
inner_join and the left_join in order to preserve the functional behaviour of the operations. 2334 
The different kinds of relational joins behave as follows. 2335 
 inner_join: the Data Points of ds1, …, dsN are joined if they have the same values for the common 2336 
Identifier Components or, if the using clause is present, for the specified Components.  A (joined) virtual 2337 
Data Point is generated in the virtual Data Set VDS1 when a matching Data Point is found for each one of the 2338 
input Data Sets. In this case, the Values of the Components of a virtual Data Point are taken from the 2339 
68 
 
corresponding Components of the matching Data Points. If there is no match for one or more input Data Sets, 2340 
no virtual Data Point is generated.  2341 
 left_join: the join is ideally performed stepwise, between consecutive pairs of input Data Sets, starting from 2342 
the left side and proceeding towards the right side. The Data Points are matched like in the inner_join, but a 2343 
virtual Data Point is generated even if no Data Point of the right Data Set matches (in this case, the Measures 2344 
and Attributes coming from the right Data Set take the NULL value in the virtual Data Set).  Therefore, for 2345 
each Data Points of the left Data Set a virtual Data Point is always generated. These stepwise operations are 2346 
associative. More formally, consider the generic pair <dsi, dsi+1>, where dsi is the result of the left_join of the 2347 
first “i” operands and dsi+1 is the i+1th operand. For each pair <dsi, dsi+1>, the joined Data Set is fed with all 2348 
the Data Points that match in dsi and dsi+1 or are only in dsi. The constraints described above guarantee the 2349 
absence of null values for the Identifier Components of the joined Data Set, whose values are always taken 2350 
from the left Data Set. If the join succeeds for a Data Point in dsi, the values for the Measures and the 2351 
Attributes are carried from dsi and dsi+1 as explained above. Otherwise, i.e., if no Data Point in dsi+1 matches 2352 
the Data Point in dsi, null values are given to Measures and Attributes coming only from dsi+1.  2353 
 full_join: the join is ideally performed stepwise, between consecutive pairs of input Data Sets, starting from 2354 
the left side and proceeding toward the right side. The Data Points are matched like in the inner_join and 2355 
left_join, but the using clause is not allowed and a virtual Data Point is generated either if no Data Point of 2356 
the right Data Set matches with the left Data Point or if no Data Point of the left Data Set matches with the 2357 
right Data Point (in this case, Measures and Attributes coming from the non matching Data Set take the NULL 2358 
value in the virtual Data Set).  Therefore, for each Data Points of the left and the right Data Set, a virtual Data 2359 
Point is always generated. These stepwise operations are associative. More formally, consider the generic 2360 
pair <dsi, dsi+1>, where dsi is the result of the full_join of the first “i” operands and dsi+1 is the i+1th operand. 2361 
For each pair <dsi, dsi+1>, the resulting Data Set is fed with the Data Points that match in dsi and dsi+1 or that 2362 
are only in dsi or in dsi+1. If for a Data Point in dsi the join succeeds, the values for the Measures and the 2363 
Attributes are carried from dsi and dsi+1 as explained. Otherwise, i.e., if no Data Point in dsi+1 matches the 2364 
Data Point in dsi, NULL values are given to Measures and Attributes coming only from dsi+1. Symmetrically, if 2365 
no Data Point in dsi matches the Data Point in dsi+1, NULL values are given to Measures and Attributes 2366 
coming only from dsi. The constraints described above guarantee the absence of NULL values on the 2367 
Identifier Components. As mentioned, the using clause is not allowed in this case.  2368 
 cross_join:  the join is performed stepwise, between consecutive pairs of input Data Sets, starting from the 2369 
left side and proceeding toward the right side. No match is performed but the Cartesian product of the input 2370 
Data Points is generated in output. These stepwise operations are associative. More formally, consider the 2371 
ordered pair <dsi, dsi+1>, where dsi is the result of the cross_ join of the first “i” operands and dsi+1 is the 2372 
i+1-th operand. For each pair <dsi, dsi+1>, the resulting Data Set is fed with the Data Points obtained as the 2373 
Cartesian product between the Data Points of dsi and dsi+1. The resulting Data Set will have all the 2374 
Components from dsi and dsi+1. For the Data Sets which have at least one Component in common, the alias 2375 
parameter is mandatory. As mentioned, the using parameter is not allowed in this case.  2376 
 2377 
The semantics of the clauses is the following. 2378 
 filter takes as input a Boolean Component expression (having type component<boolean>). This clause 2379 
filters in or out the input Data Points; when the expression is TRUE the Data Point is kept, otherwise it is 2380 
not kept in the result. Only one filter clause is allowed.  2381 
 apply combines the homonym Measures in the source operands whose type is compatible with the 2382 
operators used in applyExpr, generating homonym Measures in the ouput. The expression applyExpr 2383 
can use as input the names or aliases of the operand Data Sets. It applies the expression to all the n-uples 2384 
of homonym Measures in the input Data Sets producing in the target a single homonym Measure for 2385 
each n-uple. It can be thought of as the multi-measure version of the calc. For example, if the following 2386 
aliases have been declared: d1, d2,  d3, then the following expression d1+d2+d3, sums all the homonym 2387 
Measures in the three input Data Sets, say M1 and M2, so as to obtain in the result: M1 := d1#M1 + 2388 
d2#M1 + d3#M1 and M2 := d1#M2 + d2#M2 + d3#M2. It is not only a compact version of a multiple 2389 
calc, but also essential when the number of Measures in the input operands is not known beforehand. 2390 
Only one apply clause is allowed.  2391 
 calc calculates new Identifier, Measure or Attribute Components on the basis of sub-expressions at 2392 
Component level. Each Component is calculated through an independent sub-expression.  It is possible 2393 
to specify the role of the calculated Component among measure, identifier, attribute, or viral 2394 
attribute, therefore the calc clause can be used also to change the role of a Component when possible. 2395 
The keyword viral allows controlling the virality of Attributes (for the Attribute propagation rule see the 2396 
User Manual). The following rule is used when the role is omitted: if the component exists in the 2397 
operand Data Set then it maintains that role; if the component does not exist in the operand Data Set 2398 
then the role is measure. The calcExpr are independent one another, they can only reference 2399 
69 
 
Components of the input Virtual Data Set and cannot use Components generated, for example, by other 2400 
calcExpr . If the calculated Component is a new Component, it is added to the output virtual Data Set. If 2401 
the Calculated component is a Measure or an Attribute that already exists in the input virtual Data Set, 2402 
the calculated values overwrite the original values. If the Calculated component is an Identifier that 2403 
already exists in the input virtual Data Set, an exception is raised because overwriting an Identifier 2404 
Component is forbidden for preserving the functional behaviour. Analytic operators can be used in the 2405 
calc clause. 2406 
 aggr calculates aggregations of dependent Components (Measures or Attributes) on the basis of  sub-2407 
expressions at Component level. Each Component is calculated through an independent sub-expression.  2408 
It is possible to specify the role of the calculated Component among measure, identifier, attribute, or 2409 
viral attribute. The substring viral allows to control the virality of Attributes, if the Attribute 2410 
propagation rule is adopted (see the User Manual). The aggr sub-expressions are independent of one 2411 
another, they can only reference Components of the input Virtual Data Set and cannot use Components 2412 
generated, for example, by other aggr sub-expressions. The aggr computed Measures and Attributes 2413 
are the only Measures and Attributes returned in the output virtual Data Set (plus the possible viral 2414 
Attributes, see below Attribute propagation). The sub-expressions must contain only Aggregate 2415 
operators, which are able to compute an aggregated Value relevant to a group of Data Points. The groups 2416 
of Data Points to be aggregated are specified through the groupingClause, which allows the following 2417 
alternative options. 2418 
group by the Data Points are grouped by the values of the specified Identifier. The Identifiers not 2419 
specified are dropped in the result. 2420 
group except the Data Points are grouped by the values of the Identifiers not specified in the clause. 2421 
The specified Identifiers are dropped in the result. 2422 
group all converts an Identifier Component using conversionExpr and keeps all the resulting 2423 
Identifiers. 2424 
The having clause is used to filter groups in the result by means of an aggregate condition evaluated on 2425 
the single groups, for example the minimum number of rows in the group.  2426 
If no grouping clause is specified, then all the input Data Points are aggregated in a single group and the 2427 
clause returns a Data Set that contains a single Data Point and has no Identifier Components. 2428 
 keep maintains in the output only the specified dependent Components (Measures and Attributes) of 2429 
the input virtual Data Set and drops the non-specified ones. It has the role of a projection in the usual 2430 
relational semantics (specifying which columns have to be projected in). Only one keep clause is 2431 
allowed. If keep is used, drop must be omitted.  2432 
 drop maintains in the output only the non-specified dependent Components (Measures and Attributes) 2433 
of the input virtual Data Set (component<scalar>) and drops the specified ones. It has the role of a 2434 
projection in the usual relational join semantics (specifying which columns will be projected out). Only 2435 
one drop clause is allowed. If drop is used, keep must be omitted.  2436 
 rename assigns new names to one or more Components (Identifier, Measure or Attribute Components). 2437 
The resulting Data Set, after renaming all the specified Components, must have unique names of all its 2438 
Components (otherwise a runtime error is raised). Only the Component name is changed and not the 2439 
Component Values, therefore the new Component must be defined on the same Value Domain and Value 2440 
Domain Subset as the original Component (see also the IM in the User Manual). If the name of a 2441 
Component defined on a different Value Domain or Set is assigned, an error is raised. In other words, 2442 
rename is a transformation of the variable without any change in its values.  2443 
The semantics of the Attribute propagation in the join is the following.  The Attributes calculated through the 2444 
calc or aggr clauses are maintained unchanged. For all the other Attributes that are defined as viral, the 2445 
Attribute propagation rule is applied (for the semantics, see the Attribute Propagation Rule section in the User 2446 
Manual). This is done before the application of the drop, keep and rename clauses, which acts also on the 2447 
Attributes resulting from the propagation.  2448 
The semantics of the final automatic aliases removal is the following. After the application of all the clauses, the 2449 
structure of the final virtual Data Set is further modified. All the Components of the form 2450 
“alias#component_name” (or “dataset_name#component_name”) are implicitly renamed into 2451 
“component_name”. This means that the prefixes in the Component names are automatically removed. It is 2452 
responsibility of the user to guarantee the absence of duplicated Component names once the prefixes are 2453 
removed. In other words, the user must ensure that there are no pairs of Components whose names are of the 2454 
form “alias1#c1” and “alias2#c1” in the structure of the virtual Data Point, since the removal of “alias1” and 2455 
“alias2” would cause the clash. If, after the aliases removal two Components have the same name, an error is 2456 
raised.  In particular, name conflicts may derive if the using clause is present and some homonym Identifier 2457 
Components do not appear in it; these components should be properly renamed because cannot be removed; the 2458 
70 
 
input Data Set have homonym Measures and there is no apply clause which unifies them; these Measures can be 2459 
renamed  or removed.  2460 
 2461 
Examples  2462 
 2463 
Given the operand Data Sets DS_1 and DS_2: 2464 
 2465 
DS_1 
Id_1 Id_2 Me_1 Me_2 
1 A A B 
1 B C D 
2 A E F 
 2466 
DS_2 
Id_1 Id_2 Me_1A Me_2 
1 A B Q 
1 B S T 
3 A Z M 
 2467 
 2468 
Example 1:   2469 
DS_r  := inner_join ( DS_1 as d1, DS_2 as d2,  2470 
keep Me_1, d2#Me_2, Me_1A)  results in: 2471 
 2472 
DS_r 
Id_1 Id_2 Me_1 Me_2 Me_1A 
1 A A Q B 
1 B C T S 
 2473 
Example 2: 2474 
  DS_r  := left_join ( DS_1 as d1, DS_2 as d2, 2475 
keep Me_1, d2#Me_2, Me_1A )  results in: 2476 
 2477 
DS_r 
Id_1 Id_2 Me_1 Me_2 Me_1A 
1 A A Q B 
1 B C T S 
2 A E null null 
 2478 
Example 3:  2479 
DS_r  := full_join ( DS_1 as d1, DS_2 as d2,  2480 
keep Me_1, d2#Me_2, Me_1A )  results in: 2481 
 2482 
DS_r 
Id_1 Id_2 Me_1 Me_2 Me_1A 
1 A A Q B 
1 B C T S 
2 A E null null 
71 
 
3 A null M Z 
 2483 
Example 4:  2484 
DS_r  := cross_join (DS_1 as d1, DS_2 as d2, 2485 
rename d1#Id_1 to Id11, d1#Id_2 to Id12, d2#Id1 to Id21, d2#Id2 to Id22, d1#Me_2 2486 
to Me12 )         2487 
results in: 2488 
 2489 
DS_r 
Id_11 Id_12 Id_21 Id_22 Me_1 Me12 Me_1A Me_2 
1 A 1 A A B B Q 
1 A 1 B A B S T 
1 A 3 A A B Z M 
1 B 1 A C D B Q 
1 B 1 B C D S T 
1 B 3 A C D Z M 
2 A 1 A E F B Q 
2 A 1 B E F S T 
2 A 3 A E F Z M 
 2490 
 2491 
Example 5:  2492 
DS_r  := inner_join (DS_1 as d1, DS_2 as d2, 2493 
filter Me_1 = “A”,  2494 
 calc Me_4 = Me_1 || Me_1A, 2495 
drop d1#Me_2)     2496 
 2497 
where || is the string concatenation,   results in: 2498 
 2499 
DS_r 
Id_1 Id_2 Me_1 Me_2 Me_1A Me_4 
1 A A Q B AB 
 2500 
 2501 
 2502 
Example 6:   2503 
DS_r  := inner_join ( DS_1 2504 
calc Me_2 := Me_2 || “_NEW” 2505 
filter Id_2 =”B” 2506 
keep Me_1, Me_2)   2507 
 2508 
where || is the string concatenation,   results in: 2509 
 2510 
DS_r 
Id_1 Id_2 Me_1 Me_2 
1 B C D_NEW 
 2511 
 2512 
Example 7:  2513 
Given the operand Data Sets DS_1 and DS_2: 2514 
 2515 
72 
 
DS_1 
Id_1 Id_2 Me_1 Me_2 
1 A A B 
1 B C D 
2 A E F 
 2516 
DS_2 
Id_1 Id_2 Me_1 Me_2 
1 A B Q 
1 B S T 
3 A Z M 
 2517 
  2518 
DS_r  := inner_join ( DS_1 as d1, DS_2 as d2,  2519 
apply d1 || d2)      2520 
 2521 
DS_r 
Id_1 Id_2 Me_1 Me_2 
1 A AB BQ 
1 B CS DT 
 2522 
 2523 
 2524 
73 
 
VTL-ML  -  String operators  2525 
String concatenation :   ||  2526 
 2527 
Syntax   2528 
op1 || op2 2529 
 2530 
Input Parameters 2531 
op1, op2 the operands 2532 
 2533 
Examples of valid syntaxes   2534 
"Hello" || ", world!"   2535 
ds_1 || ds_2 2536 
 2537 
Semantics for scalar operations 2538 
Concatenates two strings.  For example,  "Hello" || ", world!"   gives  "Hello, world!"   2539 
 2540 
Input parameters type  2541 
op1, op2 :: dataset   { measure<string>   _+ } 2542 
|   component<string> 2543 
|   string       2544 
 2545 
Result type 2546 
result ::   dataset   { measure<string>   _+ } 2547 
|   component<string> 2548 
|   string       2549 
 2550 
Additional constraints 2551 
None. 2552 
 2553 
Behaviour  2554 
The operator has the behaviour of the “Operators applicable on two Scalar Values or Data Sets or Data Set 2555 
Components” (see the section “Typical behaviours of the ML Operators”).   2556 
 2557 
Examples  2558 
Given the Data_Sets DS_1 and DS_2: 2559 
 2560 
DS_1 
Id_1 Id_2 Me_1 
1 A "hello" 
2 B "hi" 
 2561 
 2562 
DS_2 
Id_1 Id_2 Me_1 
1 A "world" 
2 B "there" 
 2563 
Example 1:  DS_r := DS_1 ||   DS_2        results in: 2564 
 2565 
74 
 
DS_r 
Id_1 Id_2 Me_1 
1 A "helloworld" 
2 B "hithere" 
 2566 
Example 2 (on component):  DS_r := DS_1[calc Me_2:=  Me_1 || “ world”]        results in: 2567 
 2568 
DS_r 
Id_1 Id_2 Me_1 Me_2 
1 A "hello" "hello world" 
2 B "hi" "hi world" 
Whitespace removal :     trim,  rtrim,  ltrim 2569 
Syntax   2570 
{trim|ltrim|rtrim}1 ( op ) 2571 
 2572 
Input parameters 2573 
op the operand 2574 
 2575 
Examples of valid syntaxes   2576 
trim("Hello ") 2577 
trim(ds_1) 2578 
 2579 
Semantics for scalar operations 2580 
Removes trailing or/and leading whitespace from a string.  For example,    trim("Hello ")   gives  "Hello".   2581 
 2582 
Input parameters type  2583 
op ::                 dataset   { measure<string>   _+ } 2584 
|   component<string> 2585 
|   string       2586 
 2587 
Result type 2588 
result ::  dataset   { measure<string>   _+ } 2589 
|   component<string> 2590 
|   string       2591 
 2592 
Additional constraints 2593 
None. 2594 
 2595 
Behaviour  2596 
The operator has the behaviour of the “Operators applicable on one Scalar Value or Data Set or Data Set 2597 
Component” (see the section “Typical behaviours of the ML Operators”).   2598 
 2599 
Examples  2600 
 2601 
Given the Data Set DS_1:  2602 
 2603 
DS_1 
Id_1 Id_2 Me_1 
1 A "hello    " 
2 B "hi     " 
 2604 
75 
 
Example 1:  DS_r := rtrim(DS_1)        results in: 2605 
 2606 
DS_r 
Id_1 Id_2 Me_1 
1 A "hello" 
2 B "hi" 
 2607 
Example 2 (on component):  DS_r := DS_1[ calc Me_2:=  rtrim(Me_1)]        results in: 2608 
 2609 
DS_r 
Id_1 Id_2 Me_1 Me_2 
1 A "hello    " "hello" 
2 B "hi     " "hi" 
Character case conversion :    upper/lower  2610 
Syntax   2611 
{upper | lower}1 ( op ) 2612 
 2613 
Input Parameters 2614 
op the operand 2615 
 2616 
Examples of valid syntaxes   2617 
upper("Hello") 2618 
lower(ds_1) 2619 
 2620 
Semantics for scalar operations 2621 
Converts the character case of a string in upper or lower case. For example,  upper("Hello")   gives  "HELLO".   2622 
 2623 
Input Parameters type  2624 
op ::                 dataset   { measure<string>   _+  } 2625 
|   component<string> 2626 
|   string       2627 
 2628 
Result type 2629 
result ::  dataset   { measure<string>   _+  } 2630 
|   component<string> 2631 
|   string       2632 
 2633 
Additional constraints 2634 
None. 2635 
 2636 
Behaviour  2637 
The operator has the behaviour of the “Operators applicable on one Scalar Value or Data Set or Data Set 2638 
Component” (see the section “Typical behaviours of the ML Operators”).   2639 
 2640 
Examples  2641 
Given the Data Set DS_1:  2642 
 2643 
DS_1 
Id_1 Id_2 Me_1 
1 A "hello" 
2 B "hi" 
76 
 
 2644 
Example 1:  DS_r := upper(DS_1)        results in: 2645 
 2646 
DS_r 
Id_1 Id_2 Me_1 
1 A "HELLO" 
2 B "HI" 
 2647 
Example 2 (on component):  DS_r := DS_1[calc Me_2:=  upper(Me_1)]        results in: 2648 
 2649 
DS_R 
Id_1 Id_2 Me_1 Me_2 
1 A "hello" "HELLO" 
2 B "hi" "HI" 
 2650 
Sub-string extraction :     substr 2651 
Syntax   2652 
substr ( op, start, length ) 2653 
 2654 
 2655 
Input parameters 2656 
op the operand 2657 
start the starting digit (first character) of the string to be extracted  2658 
length the length (number of characters) of the string to be extracted 2659 
 2660 
Examples of valid syntaxes   2661 
substr  ( DS_1,  2 ,  3 ) 2662 
substr  ( DS_1, 2 )  2663 
substr  ( DS_1, _ , 3 ) 2664 
substr  ( DS_1 )  2665 
 2666 
Semantics for scalar operations 2667 
The operator extracts a substring from op, which must be string type. The substring starts from the startth 2668 
character of the input string and has a number of characters equal to the length parameter.  2669 
 If start is omitted, the substring starts from the 1st position. 2670 
 If length is omitted or overcomes the length of the input string, the substring ends at the end of the input 2671 
string.  2672 
 If start is greater than the length of the input string, an empty string is extracted. 2673 
 2674 
For example: 2675 
substr (“abcdefghijklmnopqrstuvwxyz”, start:= 5 , length:= 10 )    gives:    “efghijklmn”. 2676 
substr (“abcdefghijklmnopqrstuvwxyz”, start:= 25 , length:= 10 )   gives:    “yz”. 2677 
substr (“abcdefghijklmnopqrstuvwxyz”, start:= 30 , length:= 10 )   gives:     “”. 2678 
 2679 
Input parameters type  2680 
op ::                 dataset   { measure <string>   _+  } 2681 
|   component <string> 2682 
|   string       2683 
 2684 
start ::   component < integer [ value >= 1 ] > 2685 
|  integer [ value >= 1 ]        2686 
 2687 
77 
 
 2688 
length ::   component < integer [ value >= 0 ] > 2689 
| integer [ value >= 0 ]   2690 
   2691 
    2692 
 2693 
Result type 2694 
result ::                 dataset   { measure<string>   _+  } 2695 
|   component<string> 2696 
|   string       2697 
 2698 
Additional constraints 2699 
None. 2700 
  2701 
Behaviour  2702 
As for the invocations at Data Set level, the operator has the behaviour of the “Operators applicable on one Scalar 2703 
Value or Data Set or Data Set Component”,  as for the invocations at Component or Scalar  level, the operator has 2704 
the behaviour of the “Operators applicable on more than two  Scalar Values or Data Set Components”, (see the 2705 
section “Typical behaviours of the ML Operators”).   2706 
 2707 
Examples  2708 
 2709 
Given the operand Data Set DS_1: 2710 
 2711 
DS_1 
Id_1 Id_2 Me_1 Me_2 
1 A "hello world" "medium size text" 
1 B "abcdefghilmno" "short text" 
2 A "pqrstuvwxyz" "this is a long description" 
 2712 
Example 1:  DS_r:= substr ( DS_1  , 7 )  results in: 2713 
 2714 
DS_r 
Id_1 Id_2 Me_1 Me_2 
1 A "world" " size text" 
1 B "ghilmno" "text" 
2 A "vwxyz" "s a long description" 
 2715 
Example 2:   DS_r:= substr ( DS_1 , 1 , 5 )  results in: 2716 
 2717 
DS_r 
Id_1 Id_2 Me_1 Me_2 
1 A "hello" "mediu" 
1 B "abcde" "short" 
2 A "pqrst" "this " 
 2718 
Example3(on Components):         DS_r:= DS_1  [ calc Me_2:=  substr ( Me_2 , 1 , 5 ) ] results in: 2719 
 2720 
DS_r 
Id_1 Id_2 Me_1 Me_2 
1 A "hello world" "mediu" 
78 
 
1 B "abcdefghilmno" "short" 
2 A "pqrstuvwxyz" "this " 
 2721 
String pattern replacement:   replace 2722 
Syntax   2723 
replace (op , pattern1,  pattern2 ) 2724 
 2725 
Input parameters 2726 
op       the operand 2727 
pattern1     the pattern to be replaced 2728 
pattern2     the replacing pattern 2729 
 2730 
Examples of valid syntaxes   2731 
replace(DS_1, "Hello", "Hi") 2732 
replace(DS_1, "Hello") 2733 
 2734 
Semantics for scalar operations 2735 
Replaces all the occurrences of a specified string-pattern (pattern1) with another one (pattern2). If pattern2 is 2736 
omitted then all occurrences of pattern1 are removed. For example: 2737 
 2738 
replace("Hello world", "Hello", "Hi") gives "Hi world" 2739 
replace("Hello world", "Hello")  gives " world" 2740 
replace ("Hello", "ello", "i")     gives "Hi" 2741 
 2742 
Input parameters type  2743 
op ::                   dataset   { measure<string>   _+ } 2744 
|   component<string> 2745 
|   string       2746 
pattern1, pattern2 :: component<string> 2747 
|  string 2748 
 2749 
Result type 2750 
result ::  dataset   { measure<string>   _+ } 2751 
|   component<string> 2752 
|   string       2753 
 2754 
Additional constraints 2755 
None. 2756 
 2757 
Behaviour  2758 
As for the invocations at Data Set level, the operator has the behaviour of the “Operators applicable on one Scalar 2759 
Value or Data Set or Data Set Component”,  as for the invocations at Component or Scalar  level, the operator has 2760 
the behaviour of the “Operators applicable on more than two  Scalar Values or Data Set Components”, (see the 2761 
section “Typical behaviours of the ML Operators”).   2762 
 2763 
Examples  2764 
Given the Data_ Set DS_1: 2765 
 2766 
DS_1 
Id_1 Id_2 Me_1 
1 A "hello world" 
2 A "say hello" 
3 A "he" 
79 
 
4 A "hello!" 
 2767 
Example 1:  DS_r := replace (ds_1,"ello","i")        results in: 2768 
 2769 
DS_r 
Id_1 Id_2 Me_1 
1 A "hi world" 
2 A "say hi" 
3 A "he" 
4 A "hi! " 
 2770 
Example 2 (on component):  DS_r := DS_1[ calc Me_2:=  replace (Me_1,"ello","i")]        results in: 2771 
 2772 
DS_r 
Id_1 Id_2 Me_1 Me_2 
1 A " hello world" "hi world" 
2 A " say hello" "say hi" 
3 A "he" "he" 
4 A "hello! " "hi! " 
 2773 
String pattern location :     instr 2774 
 2775 
Syntax   2776 
instr ( op, pattern, start, occurrence )    2777 
 2778 
 2779 
Input parameters 2780 
op        the operand 2781 
pattern         the string-pattern to be searched 2782 
start        the position in the input string of the character from which the search starts 2783 
occurrence       the occurrence of the pattern to search 2784 
 2785 
Examples of valid syntaxes   2786 
instr ( DS_1,  “ab”, 2 , 3 ) 2787 
instr ( DS_1,  “ab”, 2 ) 2788 
instr ( DS_1,  “ab”, _ , 2 ) 2789 
instr ( DS_1,  “ab” ) 2790 
 2791 
Semantics for scalar operations 2792 
The operator returns the position in the input string of a specified string (pattern). The search starts from the 2793 
startth character of the input string and finds the nthoccurrence of the pattern, returning the position of its first 2794 
character.  2795 
 If start is omitted, the search starts from the 1st position. 2796 
 If nthoccurrence is omitted, the value is 1. 2797 
If the nthoccurrence of the string-pattern after the startth character is not found in the input string, the returned 2798 
value is 0. 2799 
 2800 
For example: 2801 
instr ("abcde", "c" )     gives 3 2802 
instr ("abcdecfrxcwsd", "c", _ , 3 )   gives 10 2803 
instr ("abcdecfrxcwsd", "c", 5 , 3 )   gives 0 2804 
80 
 
 2805 
Input parameters type  2806 
op ::                 dataset   { measure<string>  _ } 2807 
|   component<string> 2808 
|   string       2809 
pattern :: component<string> 2810 
|  string 2811 
start ::                component < integer [ value >= 1 ] >  2812 
|  integer [ value >= 1 ]        2813 
occurrence :: component < integer [ value >= 1 ] >  2814 
|  integer [ value >= 1 ]        2815 
 2816 
Result type 2817 
result ::                 dataset   { measure<integer[value >= 0]>  int_var  } 2818 
|   component<integer[value >= 0]> 2819 
|   integer[value >= 0]       2820 
 2821 
Additional constraints 2822 
For operations at Data Set level, the input Data Set must have exactly one string type Measure. 2823 
 2824 
Behaviour  2825 
As for the invocations at Data Set level, the operator has the behaviour of the “Operators applicable on one Scalar 2826 
Value or Data Set or Data Set Component”,  as for the invocations at Component or Scalar  level, the operator has 2827 
the behaviour of the “Operators applicable on more than two  Scalar Values or Data Set Components”, (see the 2828 
section “Typical behaviours of the ML Operators”).  2829 
If op is a Data Set then instr returns a dataset with a single measure int_var of type integer. 2830 
 2831 
Examples 2832 
Given the Data Set DS_1: 2833 
 2834 
DS_1 
Id_1 Id_2 Me_1 
1 A "hello world" 
2 A "say hello" 
3 A "he" 
4 A "hi, hello! " 
 2835 
Example 1:  DS_r:= instr(ds_1,”hello”)    results in 2836 
 2837 
DS_r 
Id_1 Id_2 int_var 
1 A 1 
2 A 5 
3 A 0 
4 A 5 
 2838 
Example 2 (on component):  DS_r := DS_1[calc Me_2:=instr(Me_1,”hello”)]    results in: 2839 
 2840 
DS_r 
Id_1 Id_2 Me_1 Me_2 
1 A “hello world” 1 
2 A “say hello” 5 
81 
 
3 A “he” 0 
4 A “hi, hello!” 5 
 2841 
 2842 
Given the Data Set DS_2: 2843 
 2844 
DS_2 
Id_1 Id_2 Me_1 Me_2 
1 A "hello" "world" 
2 B NULL "hi" 
 2845 
Example 3 (applying the instr operator at component level to a multi Measure Data Set):    2846 
 2847 
DS_r := DS_2 [calc Me_10:= instr(Me_1, "o" ), Me_20:=instr(Me_2, "o")]   results in: 2848 
 2849 
DS_r 
Id_1 Id_2 Me_1 Me_2 Me_10 Me_20 
1 A "hello" "world" 5 2 
2 B NULL "hi" null 0 
 2850 
 2851 
Example 4 (applying the instr operator at Data Set level to a multi Measure Data Set):    2852 
 2853 
DS_r :=  instr(DS_2, "o" )   would give error because DS_2 has more Measures. 2854 
 2855 
String length :    length  2856 
Syntax   2857 
length ( op ) 2858 
 2859 
Input Parameters 2860 
op the operand 2861 
 2862 
Examples of valid syntaxes   2863 
length("Hello, World!")   2864 
length(DS_1) 2865 
 2866 
Semantics for scalar operations 2867 
Returns the length of a string.  For example,  length("Hello, World!")  gives  13 2868 
For the empty string “” the value 0 is returned 2869 
 2870 
Input Parameters type  2871 
 op ::      dataset   { measure<string>  _  } 2872 
|   component<string> 2873 
|   string       2874 
 2875 
Result type 2876 
result ::   dataset   { measure<integer[value >= 0]>  int_var  } 2877 
|   component<integer[value >= 0]> 2878 
|   integer[value >= 0]       2879 
 2880 
82 
 
Additional constraints 2881 
For operations at Data Set level, the input Data Set must have exactly one string type Measure. 2882 
 2883 
Behaviour  2884 
The operator has the behaviour of the “Operators changing the data type” (see the section “Typical behaviours of 2885 
the ML Operators”).   2886 
If op is a Data Set then length returns a dataset with a single measure int_var of type integer. 2887 
 2888 
Examples  2889 
 2890 
Given the Data Set DS_1 2891 
 2892 
DS_1 
Id_1 Id_2 Me_1 
1 A "hello" 
2 B null 
 2893 
Example 1:  DS_r := length(DS_1)   results in:  2894 
 2895 
DS_r 
Id_1 Id_2 int_var 
1 A 5 
2 B null 
 2896 
 2897 
Example 2 (on component):   DS_r:= DS_1[calc Me_2:=length(Me_1)]   results in 2898 
 2899 
DS_r 
Id_1 Id_2 Me_1 Me_2 
1 A "hello" 5 
2 B null null 
 2900 
Given the Data Set DS_2: 2901 
 2902 
DS_2 
Id_1 Id_2 Me_1 Me_2 
1 A "hello" "world" 
2 B null "hi" 
 2903 
Example 3 (applying the length operator at component level to a multi Measure Data Set):    2904 
 2905 
DS_r := DS_2 [calc Me_10:= length(Me_1), Me_20:=length(Me_2)]   results in: 2906 
 2907 
DS_r 
Id_1 Id_2 Me_1 Me_2 Me_10 Me_20 
1 A "hello" "world" 5 5 
2 B null "hi" null 2 
83 
 
 2908 
 2909 
Example 4 (length operator applied at Data Set level to a multi Measure Data Set):    2910 
 2911 
DS_r :=  length(DS_2)   would give error because DS_2 has more Measures. 2912 
84 
 
VTL-ML  -  Numeric operators  2913 
Unary plus :   +  2914 
Syntax   2915 
+ op 2916 
 2917 
Input parameters 2918 
op the operand 2919 
 2920 
Examples of valid syntaxes   2921 
+ DS_1 2922 
+ 3 2923 
 2924 
Semantics for scalar operations 2925 
The operator + returns the operand unchanged. For example: 2926 
+ 3    gives        3 2927 
+ ( - 5 )   gives  - 5 2928 
 2929 
Input Parameters type  2930 
 op ::      dataset   { measure<number>   _+  } 2931 
|   component<number> 2932 
|   number     2933 
 2934 
Result type 2935 
result ::   dataset   { measure<number>   _+  } 2936 
|   component<number> 2937 
|   number     2938 
 2939 
Additional constraints 2940 
None. 2941 
 2942 
Behaviour  2943 
The operator has the behaviour of the “Operators applicable on one Scalar Value or Data Set or Data Set 2944 
Component” (see the section “Typical behaviours of the ML Operators”).   2945 
According to the general rules about data types, the operator can be applied also on sub-types of number, that is 2946 
the type integer. If the type of the operand is integer then the result has type integer. If the type of the operand is 2947 
number then the result has type number. 2948 
 2949 
Examples  2950 
Given the operand Data Set DS_1: 2951 
 2952 
DS_1 
Id_1 Id_2 Me_1 Me_2 
10 A 1.0 5 
10 B 2.3 10 
11 A 3.2 12 
 2953 
Example 1:  DS_r  := + DS_1  results in:  2954 
 2955 
DS_r 
Id_1 Id_2 Me_1 Me_2 
10 A 1.0 5 
85 
 
10 B 2.3 10 
11 A 3.2 12 
 2956 
Example 2  (on components):   DS_r  := DS_1 [calc  Me_3 :=  + Me_1  ] results in: 2957 
 2958 
DS_r 
Id_1 Id_2 Me_1 Me_2 Me_3 
10 A 1.0 5 1.0 
10 B 2.3 10 2.3 
11 A 3.2 12 3.2 
Unary minus:   -  2959 
Syntax   2960 -  op 2961 
 2962 
Input parameters 2963 
op the operand 2964 
 2965 
Examples of valid syntaxes   2966 - DS_1 2967 - 3 2968 
 2969 
Semantics for scalar operations 2970 
The operator - inverts the sign of op. For example: 2971 -  3   gives  - 3 2972 - ( - 5 )  gives     5 2973 
 2974 
Input Parameters type  2975 
 op ::      dataset   { measure<number>   _+  } 2976 
|   component<number> 2977 
|   number     2978 
 2979 
Result type 2980 
result ::       dataset   { measure<number>   _+  } 2981 
|   component<number> 2982 
|   number     2983 
 2984 
Additional constraints 2985 
None. 2986 
 2987 
Behaviour  2988 
The operator has the behaviour of the “Operators applicable on one Scalar Value or Data Set or Data Set 2989 
Component” (see the section “Typical behaviours of the ML Operators”).   2990 
According to the general rules about data types, the operator can be applied also on sub-types of number, that is 2991 
the type integer. If the type of the operand is integer then the result has type integer. If the type of the operand is 2992 
number then the result has type number. 2993 
 2994 
Examples  2995 
Given the operand Data Set DS_1: 2996 
 2997 
DS_1 
Id_1 Id_2 Me_1 Me_2 
10 A 1 5.0 
86 
 
10 B 2 10.0 
11 A 3 12.0 
 2998 
Example 1:  DS_r  := - DS_1  results in:  2999 
 3000 
DS_r 
Id_1 Id_2 Me_1 Me_2 
10 A -1 -5.0 
10 B -2 -10.0 
11 A -3 -12.0 
 3001 
Example 2 (on components):   DS_r  := DS_1 [  calc  Me_3  :=  -  Me_1  ]  results in: 3002 
 3003 
DS_r 
Id_1 Id_2 Me_1 Me_2 Me_3 
10 A 1 5.0 -1 
10 B 2 10.0 -2 
11 A 3 12.0 -3 
 3004 
 3005 
Addition :   + 3006 
Syntax   3007 
op1 + op2 3008 
 3009 
Input parameters 3010 
op1 the first addendum 3011 
op2 the second addendum 3012 
 3013 
Examples of valid syntaxes   3014 
DS_1 + DS_2 3015 
3 + 5 3016 
 3017 
Semantics for scalar operations 3018 
The operator addition returns the sum of two numbers. For example: 3019 
3 + 5   gives  8 3020 
 3021 
Input parameters type  3022 
 op1, op2 ::     dataset   { measure<number>   _+  } 3023 
|   component<number> 3024 
|   number     3025 
 3026 
Result type 3027 
result ::       dataset   { measure<number>   _+  } 3028 
|   component<number> 3029 
|   number     3030 
 3031 
Additional constraints 3032 
None. 3033 
 3034 
87 
 
Behaviour  3035 
The operator has the behaviour of the “Operators applicable on two Scalar Values or Data Sets or Data Set 3036 
Components” (see the section “Typical behaviours of the ML Operators”).   3037 
According to the general rules about data types, the operator can be applied also on sub-types of number, that is 3038 
the type integer. If the type of both operands is integer then the result has type integer. If one of the operands is 3039 
of type number, then the other operand is implicitly cast to number and therefore the result has type number. 3040 
 3041 
Examples  3042 
Given the operand Data Sets DS_1 and DS_2: 3043 
 3044 
DS_1 
Id_1 Id_2 Me_1 Me_2 
10 A 5 5.0 
10 B 2 10.5 
11 A 3 12.2 
11 B 4 20.3 
 3045 
DS_2 
Id_1 Id_2 Me_1 Me_2 
10 A 10 3.0 
10 C 11 6.2 
11 B 6 7.0 
 3046 
Example 1:  DS_r  :=  DS_1  +  DS_2  results in:  3047 
 3048 
DS_r 
Id_1 Id_2 Me_1 Me_2 
10 A 15 8.0 
11 B 10 27.3 
 3049 
Example 2:   DS_r  :=  DS_1  +  3   results in: 3050 
 3051 
DS_r 
Id_1 Id_2 Me_1 Me_2 
10 A 8 8.0 
10 B 5 13.5 
11 A 6 15.2 
11 B 7 23.3 
 3052 
Example 3 (on components):  DS_r  :=  DS_1 [ calc Me_3 :=  Me_1  +  3.0 ] results in: 3053 
 3054 
DS_r 
Id_1 Id_2 Me_1 Me_2 Me_3 
10 A 5 5.0 8.0 
10 B 2 10.5 5.0 
11 A 3 12.2 6.0 
11 B 4 20.3 7.0 
88 
 
Subtraction :   - 3055 
Syntax   3056 
op1 - op2 3057 
 3058 
Input Parameters 3059 
op1 the minuend 3060 
op2 the subtrahend 3061 
 3062 
Examples of valid syntaxes   3063 
DS_1 - DS_2 3064 
3 - 5 3065 
 3066 
Semantics for scalar operations 3067 
The operator subtraction returns the difference of two numbers.  For example: 3068 
3 - 5    gives   - 2 3069 
 3070 
Input Parameters type  3071 
 op1, op2::     dataset   { measure<number>   _+  } 3072 
|   component<number> 3073 
|   number     3074 
 3075 
Result type 3076 
result ::       dataset   { measure<number>   _+  } 3077 
|   component<number> 3078 
|   number     3079 
 3080 
Additional constraints 3081 
None. 3082 
 3083 
Behaviour  3084 
The operator has the behaviour of the “Operators applicable on two Scalar Values or Data Sets or Data Set 3085 
Components” (see the section “Typical behaviours of the ML Operators”).   3086 
According to the general rules about data types, the operator can be applied also on sub-types of number, that is 3087 
the type integer. If the type of both operands is integer then the result has type integer. If one of the operands is 3088 
of type number, then the other operand is implicitly cast to number and therefore the result has type number. 3089 
 3090 
Examples  3091 
Given the operand Data Sets DS_1 and DS_2: 3092 
 3093 
DS_1 
Id_1 Id_2 Me_1 Me_2 
10 A 5 5.0 
10 B 2 10.5 
11 A 3 12.2 
11 B 4 20.3 
 3094 
DS_2 
Id_1 Id_2 Me_1 Me_2 
10 A 10 3.0 
10 C 11 6.2 
11 B 6 7.0 
 3095 
Example 1:  DS_r  :=  DS_1  -  DS_2 results in:  3096 
89 
 
 3097 
DS_r 
Id_1 Id_2 Me_1 Me_2 
10 A -5 2.0 
11 B -2 13.3 
 3098 
Example 2:   DS_r   :=  DS_1  -  3  results in: 3099 
 3100 
DS_r 
Id_1 Id_2 Me_1 Me_2 
10 A 2 2.0 
10 B -1 7.5 
11 A 0 9.2 
11 B 1 17.3 
 3101 
Example 3 (on components):  DS_r  :=  DS_1  [ calc Me_3 :=  Me_1  -  3 ]  results in: 3102 
 3103 
DS_r 
Id_1 Id_2 Me_1 Me_2 Me_3 
10 A 5 5.0 2 
10 B 2 10.5 -1 
11 A 3 12.2 0 
11 B 4 20.3 1 
 3104 
Multiplication :   * 3105 
Syntax   3106 
op1  *  op2 3107 
 3108 
Input parameters 3109 
op1 the multiplicand 3110 
op2 the multiplier 3111 
 3112 
Examples of valid syntaxes   3113 
DS_1  *  DS_2 3114 
3  *  5 3115 
 3116 
Semantics for scalar operations 3117 
The operator multiplication returns the product of two numbers. For example: 3118 
3 * 5    gives   15 3119 
 3120 
Input parameters type  3121 
 op1, op2 ::     dataset   { measure<number>   _+  } 3122 
|   component<number> 3123 
|   number     3124 
 3125 
Result type 3126 
result ::       dataset   { measure<number>   _+  } 3127 
|   component<number> 3128 
|   number     3129 
90 
 
 3130 
Additional constraints 3131 
None. 3132 
 3133 
Behaviour  3134 
The operator has the behaviour of the “Operators applicable on two Scalar Values or Data Sets or Data Set 3135 
Components” (see the section “Typical behaviours of the ML Operators”).   3136 
According to the general rules about data types, the operator can be applied also on sub-types of number, that is 3137 
the type integer. If the type of both operands is integer then the result has type integer. If one of the operands is 3138 
of type number, then the other operand is implicitly cast to number and therefore the result has type number. 3139 
 3140 
Examples  3141 
Given the operand Data Sets DS_1 and DS_2: 3142 
 3143 
DS_1 
Id_1 Id_2 Me_1 Me_2 
10 A 100 7.6 
10 B 10 12.3 
11 A 20 25.0 
11 B 2 20.0 
 3144 
DS_2 
Id_1 Id_2 Me_1 Me_2 
10 A 1 2.0 
10 C 5 3.0 
11 B 2 1.0 
 3145 
Example 1:   DS_r  :=  DS_1  *   DS_2 results in:  3146 
 3147 
DS_r 
Id_1 Id_2   Me_1 Me_2 
10 A 100 15.2 
11 B 4 20.0 
 3148 
Example 2:  DS_r  :=  DS_1  *   -3  results in: 3149 
 3150 
DS_r 
Id_1 Id_2   Me_1 Me_2 
10 A -300 -22.8 
10 B -30 -36.9 
11 A -60 -75.0 
11 B -6 -60.0 
 3151 
 3152 
Example 3 (on components):  DS_r  :=  DS_1  [ calc Me_3 :=  Me_1  * Me_2 ]  results in: 3153 
 3154 
91 
 
DS_r 
Id_1 Id_2   Me_1 Me_2 Me_3 
10 A 100 7.6 760.0 
10 B 10 12.3 123.0 
11 A 20 25.0 500.0 
11 B 2 20.0 40.0 
 3155 
Division :   / 3156 
Syntax   3157 
op1  /  op2 3158 
 3159 
Input parameters 3160 
op1 the dividend 3161 
op2 the divisor 3162 
 3163 
Examples of valid syntaxes   3164 
DS_1 / DS_2 3165 
3 / 5 3166 
 3167 
Semantics for scalar operations 3168 
The operator division divides two numbers. For example: 3169 
3 / 5    gives  0.6 3170 
 3171 
Input parameters type  3172 
 op1, op2 :: dataset   { measure<number>  _+  } 3173 
|   component<number> 3174 
|   number     3175 
 3176 
Result type 3177 
result ::       dataset   { measure<number>  _+  } 3178 
|   component<number> 3179 
|   number     3180 
 3181 
Additional constraints 3182 
None. 3183 
 3184 
Behaviour  3185 
The operator has the behaviour of the “Operators applicable on two Scalar Values or Data Sets or Data Set 3186 
Components” (see the section “Typical behaviours of the ML Operators”).   3187 
According to the general rules about data types, the operator can be applied also on sub-types of number, that is 3188 
the type integer. The result has type number. 3189 
If op2 is 0 then the operation generates a run-time error. 3190 
 3191 
Examples  3192 
Given the operand Data Sets DS_1 and DS_2: 3193 
 3194 
DS_1 
Id_1 Id_2 Me_1 Me_2 
10 A 100 7.6 
10 B 10 12.3 
92 
 
11 A 20 25.0 
11 B 10 12.3 
 3195 
DS_2 
Id_1 Id_2 Me_1 Me_2 
10 A 1 2.0 
10 C 5 3.0 
11 B 2 1.0 
 3196 
Example 1:  DS_r  :=  DS_1  /  DS_2  results in:  3197 
 3198 
DS_r 
Id_1 Id_2 Me_1 Me_2 
10 A 100 3.8 
11 B 10 25.0 
 3199 
Example 2:  DS_r  :=  DS_1  /  10  results in: 3200 
 3201 
DS_r 
Id_1 Id_2   Me_1 Me_2 
10 A 10 0.76 
10 B 1 1.23 
11 A 2 2.5 
11 B 0.2 2.0 
 3202 
Example 3 (on components):  DS_r  :=  DS_1  [ calc Me_3 :=  Me_2  /  Me_1 ]  results in: 3203 
 3204 
DS_r 
Id_1 Id_2   Me_1 Me_2 Me_3 
10 A 100 7.6 0.076 
10 B 10 12.3 1.23 
11 A 20 25.0 1.25 
11 B 2 20.0 10.0 
 3205 
Modulo :  mod 3206 
Syntax   3207 
mod ( op1 ,  op2 ) 3208 
 3209 
Input parameters 3210 
op1  the dividend 3211 
op2  the divisor 3212 
 3213 
Examples of valid syntaxes   3214 
93 
 
mod ( DS_1, DS_2 ) 3215 
mod ( DS_1, 5 ) 3216 
mod ( 5, DS_2 ) 3217 
mod ( 5, 2 ) 3218 
 3219 
Semantics for scalar operations 3220 
The operator mod returns the remainder of op1 divided by op2. It returns op1 if divisor op2 is 0. For example: 3221 
mod ( 5, 2 )  gives  1 3222 
mod ( 5, -2 )  gives -1 3223 
mod ( 8, 2 )  gives  0 3224 
mod ( 9, 0 )  gives  9 3225 
 3226 
Input Parameters type  3227 
 op1, op2 ::   dataset   { measure<number> _+  } 3228 
|   component<number> 3229 
|   number 3230 
divisor ::  number 3231 
 3232 
Result type 3233 
result ::        dataset   { measure<number> _+  } 3234 
|   component<number> 3235 
|   number 3236 
 3237 
Additional constraints 3238 
None. 3239 
 3240 
Behaviour  3241 
The operator has the behaviour of the “Operators applicable on two Scalar Values or Data Sets or Data Set 3242 
Components” (see the section “Typical behaviours of the ML Operators”).   3243 
According to the general rules about data types, the operator can be applied also on sub-types of number, that is 3244 
the type integer. If the type of both operands is integer then the result has type integer. If one of the operands is 3245 
of type number, then the other operand is implicitly cast to number and therefore the result has type number. 3246 
 3247 
Examples  3248 
Given the operand Data Sets DS_1 and DS_2: 3249 
 3250 
DS_1 
Id_1 Id_2 Me_1 Me_2 
10 A 100 0.7545 
10 B 10 18.45 
11 A 20 1.87 
11 B 9 12.3 
 3251 
DS_2 
Id_1 Id_2 Me_1 Me_2 
10 A 1 0.25 
10 C 5 3.0 
11 B 2 2.0 
 3252 
 3253 
Example 1:  DS_r  := mod ( DS_1, DS_2 )  results in:  3254 
 3255 
94 
 
DS_r 
Id_1 Id_2 Me_1 Me_2 
10 A 0 0.0045 
11 B 1 0.3 
 3256 
Example 2:  DS_r  := mod ( DS_1, 15 )  results in:  3257 
 3258 
DS_r 
Id_1 Id_2 Me_1 Me_2 
10 A 10 0.7545 
10 B 10 3.45 
11 A 5 1.87 
11 B 9 12.3 
 3259 
Example 3 (on components): DS_r  := DS_1[ calc Me_3 := mod( DS_1#Me_1,  3.0 ) ] results in:  3260 
 3261 
DS_r 
Id_1 Id_2 Me_1 Me_2 ME_3 
10 A 100 0.7545 1.0 
10 B 10 18.45 1.0 
11 A 20 1.87 2.0 
11 B 9 12.3 0.0 
 3262 
Rounding :  round 3263 
Syntax   3264 
round ( op , numDigit  ) 3265 
 3266 
Input parameters 3267 
op  the operand 3268 
numDigit the number of positions to round to 3269 
 3270 
Examples of valid syntaxes   3271 
round ( DS_1 ,  2 ) 3272 
round ( DS_2 ) 3273 
round ( 3.14159 ,  2 ) 3274 
round ( 3.14159 ,  _ ) 3275 
 3276 
Semantics for scalar operations 3277 
The operator round rounds the operand to a number of positions at the right of the decimal point equal to the 3278 
numDigit parameter. The decimal point is assumed to be at position 0. If numDigit is negative, the rouding 3279 
happens at the left of the decimal point.  The rounding operation leaves the numDigit position unchanged if the  3280 
numDigit+1 position is between 0 and 4, otherwise it adds 1 to the number that is in the numDigit position. All 3281 
the positions greater than numDigit are set to 0. The basic scalar type of the result is integer if numDigit is 3282 
omitted, number otherwise.  3283 
For example: 3284 
round ( 3.14159,  2 )    gives   3.14 3285 
round ( 3.14159,  4 )    gives   3.1416 3286 
round ( 12345.6,  0 )   gives   12346.0 3287 
95 
 
round ( 12345.6 )     gives   12346 3288 
round ( 12345.6, _ )     gives   12346 3289 
round ( 12345.6,  -1 )    gives   12350.0 3290 
 3291 
Input parameters type  3292 
 op1 ::  dataset   { measure<number>   _+  } 3293 
| component<number> 3294 
| number     3295 
numDigit:: component < integer > 3296 
|  integer  3297 
 3298 
Result type 3299 
result ::   dataset   { measure<number>   _+  } 3300 
| component<number> 3301 
| number     3302 
 3303 
Additional constraints 3304 
None. 3305 
 3306 
Behaviour  3307 
As for the invocations at Data Set level, the operator has the behaviour of the “Operators applicable on one Scalar 3308 
Value or Data Set or Data Set Component”,  as for the invocations at Component or Scalar  level, the operator has 3309 
the behaviour of the “Operators applicable on two Scalar Values or Data Sets or Data Set Components”, (see the 3310 
section “Typical behaviours of the ML Operators”).   3311 
 3312 
Examples  3313 
Given the operand Data Set DS_1: 3314 
 3315 
DS_1 
Id_1 Id_1 Me_1 Me_2 
10 A 7.5 5.9 
10 B  7.1 5.5 
11 A 36.2 17.7 
11 B 44.5 24.3 
 3316 
Example 1: DS_r  := round(DS_1, 0)  results in:  3317 
 3318 
DS_r 
Id_1 Id_2 Me_1 Me_2 
10 A 8.0 6.0 
10 B  7.0 6.0 
11 A 36.0 18.0 
11 B 45.0 24.0 
 3319 
Example 2 (on components): DS_r  := DS_1 [ calc Me_10:= round( Me_1 ) ]  results in:  3320 
 3321 
DS_r 
Id_1 Id_2 Me_1 Me_2 Me_10 
10 A 7.5 5.9 8 
10 B  7.1 5.5 7 
11 A 36.2 17.7 36 
96 
 
11 B 44.5 24.3 45 
 3322 
Example 3 (on components) : DS_r  := DS_1 [ calc Me_20:= round( Me_1 , -1 ) ]  results in:  3323 
 3324 
DS_r 
Id_1 Id_2 Me_1 Me_2 Me_20 
10 A 7.5 5.9 10 
10 B  7.1 5.5 10 
11 A 36.2 17.7 40 
11 B 44.5 24.3 40 
 3325 
Truncation :  trunc 3326 
Syntax   3327 
trunc ( op , numDigit ) 3328 
 3329 
Input Parameters 3330 
op  the operand 3331 
numDigit the number of position from which to trunc 3332 
 3333 
Examples of valid syntaxes   3334 
trunc ( DS_1 , 2 ) 3335 
trunc ( DS_1  ) 3336 
trunc ( 3.14159 , 2 ) 3337 
trunc ( 3.14159 , _ ) 3338 
 3339 
Semantics for scalar operations 3340 
The operator trunc truncates the operand to a number of positions at the right of the decimal point equal to the 3341 
numDigit parameter. The decimal point is assumed to be at position 0. If numDigit is negative, the truncation 3342 
happens at the left of the decimal point.  The truncation operation leaves the numDigit position unchanged. All 3343 
the positions greater than numDigit are eliminated. The basic scalar type of the result is integer if numDigit is 3344 
omitted, number otherwise.  3345 
For example: 3346 
trunc ( 3.14159,  2 )    gives   3.14 3347 
trunc ( 3.14159,  4 )    gives   3.1415 3348 
trunc ( 12345.6,  0 )   gives   12345.0 3349 
trunc ( 12345.6 )     gives   12345 3350 
trunc ( 12345.6, _ )     gives   12345 3351 
trunc( 12345.6,  -1 )    gives   12340.0 3352 
 3353 
Input parameters type  3354 
 op ::  dataset   { measure<number>   _+  } 3355 
|   component<number> 3356 
|   number     3357 
numDigit :: component < integer > 3358 
|  integer 3359 
 3360 
Result type 3361 
result ::   dataset   { measure<number>   _+  } 3362 
|   component<number> 3363 
|   number 3364 
 3365 
Additional constraints 3366 
None. 3367 
 3368 
97 
 
Behaviour  3369 
As for the invocations at Data Set level, the operator has the behaviour of the “Operators applicable on one Scalar 3370 
Value or Data Set or Data Set Component”,  as for the invocations at Component or Scalar  level, the operator has 3371 
the behaviour of the “Operators applicable on two Scalar Values or Data Sets or Data Set Components”, (see the 3372 
section “Typical behaviours of the ML Operators”).   3373 
 3374 
Examples  3375 
 3376 
Given the operand Data Set DS_1: 3377 
 3378 
DS_1 
Id_1 Id_1 Me_1 Me_2 
10 A 7.5 5.9 
10 B  7.1 5.5 
11 A 36.2 17.7 
11 B 44.5 24.3 
 3379 
Example 1: DS_r  := trunc(DS_1, 0)  results in:  3380 
 3381 
DS_r 
Id_1 Id_2 Me_1 Me_2 
10 A 7.0 5.0 
10 B  7.0 5.0 
11 A 36.0 17.0 
11 B 44.0 24.0 
 3382 
Example 2 (on components): DS_r  := DS_1[ calc Me_10:= trunc( Me_1 ) ]  results in:  3383 
 3384 
DS_r 
Id_1 Id_2 Me_1 Me_2 Me_10 
10 A 7.5 5.9 7 
10 B  7.1 5.5 7 
11 A 36.2 17.7 36 
11 B 44.5 24.3 44 
 3385 
Example 3 (on components): DS_r  := DS_1[ calc Me_20:= trunc( Me_1 , -1 ) ] results in:  3386 
 3387 
DS_r 
Id_1 Id_2 Me_1 Me_2 Me_20 
10 A 7.5 5.9 0 
10 B  7.1 5.5 0 
11 A 36.2 17.7 30 
11 B 44.5 24.3 40 
 3388 
98 
 
Ceiling :  ceil 3389 
Syntax   3390 
ceil ( op ) 3391 
 3392 
Input parameters 3393 
op the operand 3394 
 3395 
Examples of valid syntaxes   3396 
ceil ( DS_1 ) 3397 
ceil ( 3.14159 ) 3398 
 3399 
Semantics for scalar operations 3400 
The operator ceil returns the smallest integer greater than or equal to op.  3401 
For example: 3402 
 ceil(  3.14159 )  gives    4 3403 
 ceil( 15 )  gives  15 3404 
 ceil( -3.1415 )  gives  -3 3405 
ceil( -0.1415 )  gives    0 3406 
 3407 
Input parameters type  3408 
op ::  dataset   { measure<number>   _+  } 3409 
|   component<number> 3410 
|   number     3411 
 3412 
Result type 3413 
result ::   dataset   { measure<integer>   _+  } 3414 
|   component< integer > 3415 
|   integer 3416 
 3417 
Additional constraints 3418 
None. 3419 
 3420 
Behaviour  3421 
The operator has the behaviour of the “Operators applicable on one Scalar Value or Data Set or Data Set 3422 
Component” (see the section “Typical behaviours of the ML Operators”).   3423 
 3424 
Examples  3425 
Given the operand Data Set DS_1: 3426 
 3427 
DS_1 
Id_1 Id_1 Me_1 Me_2 
10 A 7.0 5.9 
10 B 0.1 -5.0 
11 A -32.2 17.7 
11 B 44.5 -0.3 
 3428 
Example 1: DS_r  := ceil (DS_1)  results in:  3429 
 3430 
DS_r 
Id_1 Id_1 Me_1 Me_2 
10 A 7 6 
10 B 1 -5 
11 A -32 18 
99 
 
11 B 45 0 
 3431 
Example 2 (on components): DS_r  := DS_1 [ Me_10 := ceil (Me_1) ]  results in:  3432 
 3433 
DS_r 
Id_1 Id_1 Me_1 Me_2 Me_10 
10 A 7.0 5.9 7 
10 B 0.1 -5.0 1 
11 A -32.2 17.7 -32 
11 B 44.5 -0.3 45 
 3434 
Floor:  floor 3435 
Syntax   3436 
floor ( op ) 3437 
 3438 
Input parameters 3439 
op the operand 3440 
 3441 
Examples of valid syntaxes   3442 
floor ( DS_1 ) 3443 
floor ( 3.14159 ) 3444 
 3445 
Semantics for scalar operations 3446 
The operator floor returns the greatest integer which is smaller than or equal to op.   3447 
For example: 3448 
floor(  3.1415 )  gives    3 3449 
floor( 15 )  gives  15 3450 
 floor( -3.1415 )  gives   -4 3451 
floor( -0.1415 )  gives   -1 3452 
 3453 
Input parameters type  3454 
op ::  dataset   { measure<number>   _+  } 3455 
|   component<number> 3456 
|   number     3457 
 3458 
Result type 3459 
result ::   dataset   { measure<integer>   _+  } 3460 
|   component< integer > 3461 
|   integer 3462 
 3463 
Additional constraints 3464 
None. 3465 
 3466 
Behaviour  3467 
The operator has the behaviour of the “Operators applicable on one Scalar Value or Data Set or Data Set 3468 
Component” (see the section “Typical behaviours of the ML Operators”).   3469 
 3470 
Examples  3471 
Given the operand Data Set DS_1: 3472 
 3473 
DS_1 
Id_1 Id_1 Me_1 Me_2 
100 
 
10 A 7.0 5.9 
10 B 0.1 -5.0 
11 A -32.2 17.7 
11 B 44.5 -0.3 
 3474 
Example 1:   DS_r  := floor ( DS_1 )  results in:  3475 
 3476 
DS_r 
Id_1 Id_1 Me_1 Me_2 
10 A 7 5 
10 B 0 -5 
11 A -33 17 
11 B 44 -1 
 3477 
Example 2 (on components): DS_r  := DS_1 [ Me_10 :=  floor (Me_1) ] results in:  3478 
 3479 
DS_r 
Id_1 Id_1 Me_1 Me_2 Me_10 
10 A 7.5 5.9 7 
10 B 0.1 -5.5 0 
11 A -32.2 17.7 -33 
11 B 44.5 -0.3 44 
Absolute value :  abs 3480 
Syntax   3481 
abs ( op ) 3482 
 3483 
Input parameters 3484 
op the operand 3485 
 3486 
Examples of valid syntaxes   3487 
abs ( DS_1 ) 3488 
abs ( -5 ) 3489 
 3490 
Semantics for scalar operations 3491 
The operator abs calculates the absolute value of a number.   3492 
For example: 3493 
abs ( -5.49 )  gives   5.49 3494 
abs (  5.49 )  gives   5.49 3495 
 3496 
Input parameters type  3497 
 3498 
op ::   dataset   { measure<number>   _+  } 3499 
|   component<number> 3500 
|   number 3501 
 3502 
Result type 3503 
 3504 
result ::   dataset   { measure<number [ value >= 0 ]>   _+  } 3505 
|   component<number [ value >= 0 ]> 3506 
101 
 
|   number [ value >= 0 ] 3507 
 3508 
Additional constraints 3509 
None. 3510 
 3511 
Behaviour  3512 
The operator has the  behaviour of the “Operators applicable on one Scalar Value or Data Set or Data Set 3513 
Component” (see the section “Typical behaviours of the ML Operators”).   3514 
 3515 
Examples  3516 
Given the operand Data Set DS_1: 3517 
 3518 
DS_1 
Id_1 Id_2 Me_1 Me_2 
10 A 0.484183 0.7545 
10 B -0.515817 -13.45 
11 A -1.000000 187.0 
 3519 
Example 1:   DS_r  := abs ( DS_1 )  results in:  3520 
 3521 
DS_r 
Id_1 Id_2 Me_1 Me_2 
10 A 0.484183 0.7545 
10 B 0.515817 13.45 
11 A 1.000000 187 
 3522 
Example 2 (on components): DS_r  := DS_1 [ Me_10 := abs(Me_1) ] results in:  3523 
 3524 
DS_r 
Id_1 Id_2 Me_1 Me_2 Me_10 
10 A 0.484183 0.7545 0.484183 
10 B -0.515817 -13.45 0.515817 
11 A -1.000000 187 1.000000 
 3525 
Exponential :  exp 3526 
Syntax   3527 
exp ( op ) 3528 
 3529 
Input parameters 3530 
op the operand 3531 
 3532 
Examples of valid syntaxes   3533 
exp ( DS_1) 3534 
exp ( 5 ) 3535 
 3536 
Semantics for scalar operations 3537 
The operator exp returns e (base of the natural logarithm) raised to the op-th power.   3538 
For example; 3539 
exp ( 5 )    gives 148.41315… 3540 
exp ( 1 )    gives  2.71828…  (the number e) 3541 
102 
 
exp ( 0 )    gives  1.0 3542 
exp ( -1 )    gives  0.36787… (the number 1/e) 3543 
 3544 
Input parameters type  3545 
op::  dataset   { measure<number>   _+  } 3546 
|   component<number> 3547 
|   number 3548 
 3549 
Result type 3550 
result ::   dataset   { measure<number[value > 0]>   _+  } 3551 
|   component<number [value > 0]> 3552 
|   number[value > 0] 3553 
 3554 
Additional constraints 3555 
None. 3556 
 3557 
Behaviour  3558 
The operator has the behaviour of the “Operators applicable on one Scalar Value or Data Set or Data Set 3559 
Component” (see the section “Typical behaviours of the ML Operators”).   3560 
 3561 
Examples  3562 
Given the operand Data Set DS_1: 3563 
 3564 
DS_1 
Id_1 Id_2 Me_1 Me_2 
10 A 5 0.7545 
10 B 8 13.45 
11 A 2 1.87 
 3565 
 3566 
Example 1:   DS_r  := exp(DS_1)    results in:  3567 
 3568 
DS_r 
Id_1 Id_2 Me_1 Me_2 
10 A 148.413 2.126547 
10 B 2980.95 693842.3 
11 A 7.38905 6.488296 
 3569 
Example 2 (on components): DS_r  := DS_1 [ Me_1 :=  exp ( Me_1 ) ]  results in:  3570 
 3571 
DS_r 
Id_1 Id_2 Me_1 Me_2 
10 A 148.413 0.7545 
10 B 2980.95 13.45 
11 A 7.389 1.87 
 3572 
Natural logarithm :  ln 3573 
Syntax   3574 
ln ( op ) 3575 
103 
 
 3576 
Input parameters 3577 
op the operand 3578 
 3579 
Examples of valid syntaxes   3580 
ln ( DS_1 ) 3581 
ln ( 148 ) 3582 
 3583 
Semantics for scalar operations 3584 
The operator ln calculates the natural logarithm of a number.  3585 
For example: 3586 
ln (148 )  gives    4.997… 3587 
ln ( e )  gives   1.0 3588 
ln ( 1 )  gives   0.0 3589 
ln ( 0,5 ) gives  -0.693… 3590 
 3591 
Input parameters type  3592 
 op ::  dataset   { measure<number [value > 0] > _+  }  3593 
|   component<number [value > 0] > 3594 
|   number [value > 0] 3595 
 3596 
Result type 3597 
result ::   dataset   { measure<number > _+  } 3598 
|   component<number > 3599 
|   number  3600 
 3601 
Additional constraints 3602 
None. 3603 
 3604 
Behaviour  3605 
The operator has the behaviour of the “Operators applicable on one Scalar Value or Data Set or Data Set 3606 
Component” (see the section “Typical behaviours of the ML Operators”).   3607 
 3608 
Examples  3609 
Given the operand Data Set DS_1: 3610 
 3611 
DS_1 
Id_1 Id_2 Me_1 Me_2 
10 A 148.413 0.7545 
10 B 2980.95 13.45 
11 A 7.38905 1.87 
 3612 
 3613 
Example 1:   DS_r  := ln(DS_1)  results in:  3614 
 3615 
DS_r 
Id_1 Id_2 Me_1 Me_2 
10 A 5.0 -0.281700 
10 B 8.0 2.598979 
11 A 2.0 0.625938 
 3616 
Example 2 (on components): DS_r  := DS_1 [ Me_2 :=  ln ( DS_1#Me_1 ) results in:  3617 
 3618 
104 
 
DS_r 
Id_1 Id_2 Me_1 Me_2 
10 A 148.413 5.0 
10 B 2980.95 8.0 
11 A 7.38905 2.0 
 3619 
Power :  power 3620 
Syntax   3621 
power ( base , exponent ) 3622 
 3623 
Input parameters 3624 
base  the operand 3625 
exponent the exponent of the power 3626 
 3627 
Examples of valid syntaxes   3628 
power ( DS_1, 2 ) 3629 
power ( 5, 2 ) 3630 
 3631 
Semantics for scalar operations 3632 
The operator power raises a number (the base) to another one (the exponent).  3633 
For example: 3634 
power ( 5,  2 )  gives 25 3635 
power ( 5,  1 )  gives   5 3636 
power ( 5,  0 )  gives   1 3637 
power ( 5, -1 )  gives   0.2 3638 
power ( -5, 3 )  gives  -125 3639 
 3640 
Input parameters type  3641 
base ::       dataset   { measure<number> _+  } 3642 
|   component<number> 3643 
|   number 3644 
exponent ::  component<number> 3645 
|  number 3646 
 3647 
Result type 3648 
result ::        dataset   { measure<number> _+  } 3649 
|   component<number> 3650 
|   number 3651 
 3652 
Additional constraints 3653 
None. 3654 
 3655 
Behaviour  3656 
As for the invocations at Data Set level, the operator has the behaviour of the “Operators applicable on one Scalar 3657 
Value or Data Set or Data Set Component”,  as for the invocations at Component or Scalar  level, the operator has 3658 
the behaviour of the “Operators applicable on two Scalar Values or Data Sets or Data Set Components”, (see the 3659 
section “Typical behaviours of the ML Operators”). 3660 
 3661 
Examples  3662 
Given the operand Data Set DS_1: 3663 
 3664 
DS_1 
Id_1 Id_2 Me_1 Me_2 
105 
 
10 A 3 0.7545 
10 B 4 13.45 
11 A 5 1.87 
 3665 
 3666 
Example 1:  DS_r  := power(DS_1, 2) results in:  3667 
 3668 
DS_r 
Id_1 Id_2 Me_1 Me_2 
10 A 9 0.56927 
10 B 16 180.9025 
11 A 25 3.4969 
 3669 
Example 2 (on components): DS_r  := DS_1[ calc Me_1 := power(Me_1, 2) ] results in:  3670 
 3671 
DS_r 
Id_1 Id_2 Me_1 Me_2 
10 A 9 0.7545 
10 B 16 13.45 
11 A 25 1.87 
 3672 
Logarithm :  log 3673 
Syntax   3674 
log ( op , num )        3675 
 3676 
Input parameters 3677 
op the base of the logarithm 3678 
num the number to which the logarithm is applied 3679 
 3680 
Examples of valid syntaxes   3681 
log ( DS_1, 2 ) 3682 
log ( 1024, 2 ) 3683 
 3684 
Semantics for scalar operations 3685 
The operator log calculates the logarithm of num base op.  3686 
For example: 3687 
log ( 1024,   2 )   gives 10 3688 
log ( 1024, 10 )   gives   3.01 3689 
 3690 
Input parameters type  3691 
op ::  dataset   { measure<number [value > 1] > _+  } 3692 
|   component<number [value > 1] > 3693 
|   number [value > 1]  3694 
num ::  component<integer [ value > 0]> 3695 
|  integer [value > 0]  3696 
 3697 
Result type 3698 
result ::   dataset   { measure<number> _+  } 3699 
|   component<number> 3700 
|   number 3701 
106 
 
 3702 
Additional constraints 3703 
None. 3704 
 3705 
Behaviour  3706 
As for the invocations at Data Set level, the operator has the behaviour of the “Operators applicable on one Scalar 3707 
Value or Data Set or Data Set Component”,  as for the invocations at Component or Scalar  level, the operator has 3708 
the behaviour of the “Operators applicable on two Scalar Values or Data Sets or Data Set Components”, (see the 3709 
section “Typical behaviours of the ML Operators”). 3710 
 3711 
Examples  3712 
Given the operand Data Set DS_1: 3713 
 3714 
DS_1 
Id_1 Id_2 Me_1 Me_2 
10 A 1024 0.7545 
10 B 64 13.45 
11 A 32 1.87 
 3715 
 3716 
Example 1:   DS_r  := log ( DS_1, 2 )    results in:  3717 
 3718 
DS_r 
Id_1 Id_2 Me_1 Me_2 
10 A 10.0 -0.40641 
10 B 6.0 3.749534 
11 A 5.0 0.903038 
 3719 
Example 2 (on components): DS_r  := DS_1 [ calc Me_1 := log (Me_1, 2)  ] results in:  3720 
 3721 
DS_r 
Id_1 Id_2 Me_1 Me_2 
10 A 10.0 0.7545 
10 B 6.0 13.45 
11 A 5.0 1.87 
 3722 
Square root :  sqrt 3723 
Syntax   3724 
sqrt ( op ) 3725 
 3726 
Input parameters 3727 
op the operand 3728 
 3729 
Examples of valid syntaxes   3730 
sqrt ( DS_1 ) 3731 
sqrt ( 5 ) 3732 
 3733 
Semantics for scalar operations 3734 
The operator sqrt calculates the square root of a number. For example: 3735 
sqrt ( 25 )   gives   5 3736 
107 
 
 3737 
Input parameters type   3738 
op ::       dataset   { measure<number [value >= 0] > _+  } 3739 
|   component<number [value >= 0] > 3740 
|   number [value >= 0]  3741 
 3742 
Result type 3743 
result ::        dataset   { measure<number[value >= 0] > _+  } 3744 
|   component<number[value >= 0] > 3745 
|   number[value >= 0] 3746 
 3747 
Additional constraints 3748 
None. 3749 
 3750 
Behaviour  3751 
The operator has the behaviour of the “Operators applicable on one Scalar Value or Data Set or Data Set 3752 
Component” (see the section “Typical behaviours of the ML Operators”).   3753 
 3754 
Examples  3755 
Given the operand Data Set DS_1: 3756 
 3757 
DS_1 
Id_1 Id_2 Me_1 Me_2 
10 A 16 0.7545 
10 B 81 13.45 
11 A 64 1.87 
 3758 
 3759 
Example 1:  DS_r  := sqrt(DS_1)  results in:  3760 
 3761 
DS_r 
Id_1 Id_2 Me_1 Me_2 
10 A 4 0.86862 
10 B 9 3.667424 
11 A 8 1.367479 
 3762 
 3763 
Example 2 (on components): DS_r  := DS_1 [ calc Me_1 := sqrt ( Me_1 ) ] results in:  3764 
 3765 
DS_r 
Id_1 Id_2 Me_1 Me_2 
10 A 4 0.7545 
10 B 9 13.45 
11 A 8 1.87 
 3766 
 3767 
 3768 
108 
 
VTL-ML  -  Comparison operators 3769 
Equal to :   = 3770 
 3771 
Syntax 3772 
left = right 3773 
 3774 
Input parameters 3775 
left the left operand 3776 
right the right operand 3777 
 3778 
Examples of valid syntaxes 3779 
DS_1 = DS_2 3780 
 3781 
Semantics for scalar operations 3782 
The operator returns TRUE if the left is equal to right,  FALSE otherwise.  3783 
For example: 3784 
5 = 9    gives:  FALSE 3785 
5 = 5    gives:  TRUE 3786 
“hello” = “hi”   gives:  FALSE 3787 
 3788 
Input parameters type 3789 
left,  3790 
right ::      dataset   {measure<scalar> _ } 3791 
|  component<scalar> 3792 
|  scalar     3793 
 3794 
Result type 3795 
result ::       dataset   {  measure<boolean>  bool_var } 3796 
|   component<boolean> 3797 
|   boolean    3798 
 3799 
Additional constraints 3800 
Operands left and right must be of the same scalar type 3801 
 3802 
Behaviour 3803 
The operator has the typical behaviour of the “Operators changing the data type” (see the section “Typical 3804 
behaviours of the ML Operators”).   3805 
 3806 
Examples 3807 
Given the operand Data Set DS_1: 3808 
 3809 
DS_1 
Id_1 Id_2 Id_3 Id_4 Me_1 
2012 B Total Total NULL 
2012 G Total Total 0.286 
2012 S Total Total 0.064 
2012 M Total Total 0.043 
2012 F Total Total 0.08 
2012 W Total Total 0.08 
 3810 
109 
 
Example 1: DS_r :=   DS_1 = 0.08  results in: 3811 
 3812 
DS_r 
Id_1 Id_2 Id_3 Id_4 bool_var 
2012 B Total Total NULL 
2012 G Total Total FALSE 
2012 S Total Total FALSE 
2012 M Total Total FALSE 
2012 F Total Total TRUE 
2012 W Total Total TRUE 
 3813 
Example 2 (on Components): DS_r := DS_1 [ calc Me_2 :=   Me_1 = 0.08 ]  results in: 3814 
 3815 
DS_r 
Id_1 Id_2 Id_3 Id_4 Me_1 Me_2 
2012 B Total Total NULL NULL 
2012 G Total Total 0.286 FALSE 
2012 S Total Total 0.064 FALSE 
2012 M Total Total 0.043 FALSE 
2012 F Total Total 0.08 TRUE 
2012 W Total Total 0.08 TRUE 
 3816 
Not equal to :   <> 3817 
 3818 
Syntax 3819 
 left  <>  right 3820 
 3821 
Input parameters 3822 
left the left operand 3823 
right the right operand 3824 
 3825 
Examples of valid syntaxes 3826 
DS_1 <> DS_2 3827 
 3828 
Semantics for scalar operations 3829 
The operator returns FALSE if the left is equal to right,  TRUE otherwise. 3830 
For example: 3831 
5 <> 9    gives: TRUE 3832 
5 <> 5    gives: FALSE 3833 
“hello” <> “hi”   gives: TRUE 3834 
 3835 
Input parameters type 3836 
left,  3837 
right ::     dataset   {measure<scalar> _ } 3838 
|  component<scalar> 3839 
|  scalar     3840 
 3841 
110 
 
Result type 3842 
result ::       dataset   {  measure<boolean>  bool_var } 3843 
|   component<boolean> 3844 
|   boolean    3845 
 3846 
Additional constraints 3847 
Operands left and right must be of the same scalar type 3848 
 3849 
Behaviour 3850 
The operator has the typical behaviour of the “Operators changing the data type” (see the section “Typical 3851 
behaviours of the ML Operators”).   3852 
 3853 
Examples 3854 
Given the operand Data Sets DS_1 and DS_2: 3855 
 3856 
DS_1 
Id_1 Id_2 Id_3 Id_4 Me_1 
G Total Percentage Total 7.1 
R Total Percentage Total NULL 
 3857 
 3858 
DS_2 
Id_1 Id_2 Id_3 Id_4 Me_1 
G Total Percentage Total 7.5 
R Total Percentage Total 3 
 3859 
Example 1: DS_r :=  DS_1 <>  DS_2  results in: 3860 
 3861 
DS_r 
Id_1 Id_2 Id_3 Id_4 bool_var 
G Total Percentage Total TRUE 
R Total Percentage Total NULL 
 3862 
Note that due to the behaviour for NULL values, if the value for Greece in the second operand had also been 3863 
NULL, then the result would still be NULL for Greece.  3864 
 3865 
Example 2 (on Components): DS_r := DS_1 [ Me_2 :=  Me_1<>7.5]  results in: 3866 
 3867 
DS_r 
Id_1 Id_2 Id_3 Id_4 Me_1 Me_2 
G Total Percentage Total 7.5 TRUE 
R Total Percentage Total 3 NULL 
 3868 
 3869 
Greater than :      >        >= 3870 
Syntax 3871 
left {  >  |  >= }1 right 3872 
 3873 
111 
 
Input parameters 3874 
left the left operand part of the comparison 3875 
right the right operand part of the comparison 3876 
 3877 
Examples of valid syntaxes 3878 
DS_1 >  DS_2 3879 
DS_1 >=  DS_2 3880 
 3881 
Semantics for scalar operations 3882 
The operator  >  returns TRUE if left is greater than right, FALSE otherwise. 3883 
The operator  >=  returns TRUE if left is greater than or equal to right, FALSE otherwise. 3884 
For example: 3885 
5 > 9    gives: FALSE 3886 
5 >= 5    gives: TRUE 3887 
“hello” > “hi”   gives: FALSE 3888 
 3889 
Input parameters type 3890 
left,  3891 
right :: dataset   {measure<scalar> _  } 3892 
|  component<scalar> 3893 
|  scalar     3894 
 3895 
Result type 3896 
result ::   dataset   {  measure<boolean>  bool_var  } 3897 
|   component<boolean> 3898 
|   boolean    3899 
 3900 
Additional constraints 3901 
Operands left and right must be of the same scalar type 3902 
  3903 
Behaviour 3904 
The operator has the typical behaviour of the “Operators changing the data type” (see the section “Typical 3905 
behaviours of the ML Operators”).   3906 
 3907 
Examples 3908 
Given the operand Data Set DS_1: 3909 
 3910 
DS_1 
Id_1 Id_2 Id_3 Id_4 Id_5 Me_1 
2 G 2011 Total Percentage NULL 
2 R 2011 Total Percentage 12.2 
2 F 2011 Total Percentage 29.5 
 3911 
Example 1:  DS_r := DS_1 > 20  results in: 3912 
 3913 
DS_r 
Id_1 Id_2 Id_3 Id_4 Id_5 bool_var 
2 G 2011 Total Percentage NULL 
2 R 2011 Total Percentage FALSE 
2 F 2011 Total Percentage TRUE 
 3914 
Example 2 (on Components):  DS_r := DS_1 [ Me_2 := Me_1 > 20 ]  results in: 3915 
 3916 
112 
 
DS_r 
Id_1 Id_2 Id_3 Id_4 Id_5 Me_1 Me_2 
2 G 2011 Total Percentage NULL NULL 
2 R 2011 Total Percentage 12.2 FALSE 
2 F 2011 Total Percentage 29.5 TRUE 
 3917 
Given the left operand Data Set: 3918 
 3919 
DS_1 
Id_1 Id_2 Id_3 Id_4 Me_1 
G Total Percentage Total 7.1 
R Total Percentage Total 42.5 
 3920 
and the right operand Data Set: 3921 
 3922 
DS_2 
Id_1 Id_2 Id_3 Id_4 Me_1 
G Total Percentage Total 7.5 
R Total Percentage Total 33.7 
 3923 
Example 3: DS_r:= DS_1 > DS_2  results in: 3924 
 3925 
DS_r 
Id_1 Id_2 Id_3 Id_4 bool_var 
G Total Percentage Total FALSE 
R Total Percentage Total TRUE 
 3926 
If the Me_1 column for Germany in the DS_2 Data Set had a NULL value the result would be: 3927 
 3928 
DS_r 
Id_1 Id_2 Id_3 Id_4 bool_var 
G Total Percentage Total NULL 
R Total Percentage Total TRUE 
 3929 
Less than :      <       <= 3930 
  3931 
Syntax 3932 
 left   {  <  |  <=  }1   right 3933 
 3934 
Input parameters 3935 
left the left operand  3936 
right the right operand  3937 
 3938 
Examples of valid syntaxes 3939 
DS_1 < DS_2 3940 
DS_1 <= DS_2 3941 
113 
 
 3942 
Semantics for scalar operations 3943 
The operator  <  returns TRUE if left is smaller than  right,  FALSE otherwise.  3944 
The operator  <=  returns TRUE if left is smaller than or equal to right,  FALSE otherwise.  3945 
For example:  3946 
5 < 4    gives: FALSE 3947 
5 <= 5    gives: TRUE 3948 
“hello” < “hi”   gives: TRUE 3949 
 3950 
Input parameters type 3951 
left, right ::    dataset   {measure<scalar> _ } 3952 
|  component<scalar> 3953 
|  scalar     3954 
 3955 
Result type 3956 
result ::       dataset   {  measure<boolean>  bool_var  } 3957 
|   component<boolean> 3958 
|   boolean    3959 
 3960 
Additional constraints 3961 
Operands left and right must be of the same scalar type 3962 
  3963 
Behaviour 3964 
The operator has the typical behaviour of the “Operators changing the data type” (see the section “Typical 3965 
behaviours of the ML Operators”).   3966 
 3967 
Examples 3968 
Given the operand Data Set DS_1: 3969 
 3970 
DS_1 
Id_1 Id_2 Id_3 Id_4 Me_1 
2012 B Total Total 11094850 
2012 G Total Total 11123034 
2012 S Total Total 46818219 
2012 M Total Total NULL 
2012 F Total Total 5401267 
2012 W Total Total 7954662 
 3971 
Example 1: DS_r := DS_1 < 15000000  results in: 3972 
 3973 
DS_r 
Id_1 Id_2 Id_3 Id_4 bool_var 
2012 B Total Total TRUE 
2012 G Total Total TRUE 
2012 S Total Total FALSE 
2012 M Total Total NULL 
2012 F Total Total TRUE 
2012 W Total Total TRUE 
 3974 
114 
 
Between :   between 3975 
 3976 
Syntax 3977 
between (op, from, to) 3978 
 3979 
Input parameters 3980 
op the Data Set to be checked 3981 
from the left delimiter 3982 
to the right delimiter 3983 
 3984 
Examples of valid syntaxes 3985 
ds2 := between(ds1, 5,10) 3986 
ds2 := ds1 [ calc m1 := between(me2, 5, 10) ] 3987 
 3988 
Semantics for scalar operations 3989 
The operator returns TRUE if op is greater than or equal to from and lower than or equal to to. In other terms, it 3990 
is a shortcut for the following: 3991 
 3992 
op >= from and op <= to 3993 
 3994 
The types of op, from and to must be compatible scalar types. 3995 
 3996 
Input parameters type 3997 
op ::  dataset   {measure<scalar> _} 3998 
|  component<scalar> 3999 
|  scalar 4000 
 4001 
from ::  scalar | component<scalar> 4002 
to ::   scalar | component<scalar> 4003 
 4004 
Result type 4005 
result ::    dataset   {  measure<booelan>  bool_var  } 4006 
|   component<boolean> 4007 
|   boolean    4008 
 4009 
Additional constraints 4010 
The type of the operand (i.e., the measure of the dataset, the type of the component, the scalar type) must be the 4011 
same as that of from and to. 4012 
 4013 
Behaviour 4014 
The operator has the typical behaviour of the “Operators changing the data type” (see the section “Typical 4015 
behaviours of the ML Operators”).   4016 
 4017 
Examples 4018 
 4019 
Given the following Data Set DS_1: 4020 
 4021 
DS_1 
Id_1 Id_2 Id_3 Id_4 Me_1 
G Total Percentage Total 6 
R Total Percentage Total -2 
 4022 
Example 1:   DS_r:= between(ds1, 5,10)  results in: 4023 
 4024 
DS_1 
Id_1 Id_2 Id_3 Id_4 bool_var 
115 
 
G Total Percentage Total TRUE 
R Total Percentage Total FALSE 
 4025 
Element of:   in  / not_in 4026 
 4027 
Syntax 4028 
op  in  collection 4029 
op  not_in  collection 4030 
 4031 
collection ::= set  |   valueDomainName 4032 
 4033 
Input parameters 4034 
op   the operand to be tested 4035 
collection   the the Set or the Value Domain which contains the values  4036 
set  the Set which contains the values (it can be a Set name or a Set literal) 4037 
valueDomainName the name of the Value Domain which contains the values 4038 
 4039 
Examples of valid syntaxes 4040 
ds := ds_2 in {1,4,6}  as usual, here the braces denote a set literal (it contains the values 1, 4 and 6) 4041 
ds := ds_3 in mySet 4042 
ds := ds_3 in myValueDomain  4043 
 4044 
Semantics for scalar operations 4045 
The in operator returns TRUE if op belongs to the collection, FALSE otherwise. 4046 
The not_in operator returns FALSE if op belongs to the collection, TRUE otherwise. 4047 
For example: 4048 
 1  in  { 1, 2, 3 }   returns  TRUE 4049 
“a” in { “c, “ab”, “bb”, “bc” } returns  FALSE 4050 
“b” not_in { “b”, ”hello”, ”c”} returns  FALSE 4051 
“b” not_in { “a”, ”hello”, ”c”} returns  TRUE 4052 
 4053 
Input parameters type 4054 
op ::    dataset   {measure<scalar> _ } 4055 
|  component<scalar> 4056 
|  scalar     4057 
collection ::  set<scalar>  | name<value_domain>  4058 
 4059 
Result type 4060 
result ::       dataset   {  measure<boolean> bool_var  } 4061 
|   component<boolean> 4062 
|   boolean    4063 
 4064 
Additional constraints 4065 
The operand must be of a basic scalar data type compatible with the basic scalar type of the collection. 4066 
 4067 
Behaviour 4068 
Semantics 4069 
The in operator evaluates to TRUE if the operand is an element of the specified collection and FALSE otherwise, 4070 
the not_in the opposite. 4071 
The operator has the typical behaviour of the “Operators changing the data type” (see the section “Typical 4072 
behaviours of the ML Operators”).   4073 
The collection can be either a set of values defined in line or a name that references an  externally defined Value 4074 
Domain or Set.  4075 
 4076 
Examples 4077 
Given the operand Data Set DS_1:  4078 
116 
 
 4079 
DS_1 
Id_1 Id_2 Me_1 
2012 BS 0 
2012 GZ 4 
2012 SQ 9 
2012 MO 6 
2012 FJ 7 
2012 CQ 2 
 4080 
Example 1:  4081 
 4082 
DS_r := DS_1 in  { “BS”, “MO”, “HH”, “PP” }  results in: 4083 
 4084 
DS_r 
Id_1 Id_2 bool_var 
2012 BS TRUE 
2012 GZ FALSE 
2012 SQ FALSE  
2012 MO TRUE  
2012 FJ FALSE 
2012 CQ FALSE 
 4085 
Example 2 (on Components):   4086 
 4087 
DS_r := DS_1 [ calc Me_2:= Me_1 in { “BS”, “MO”, “HH”, “PP” }]    results in: 4088 
 4089 
DS_r 
Id_1 Id_2 Me_1 Me_2 
2012 BS 0 TRUE 
2012 GZ 4 FALSE  
2012 SQ 9 FALSE  
2012 MO 6 TRUE  
2012 FJ 7 FALSE 
2012 CQ 2 FALSE 
 4090 
Given the previos Data Set DS_1 and the following Value Domain named  myGeoValueDomain (which has the 4091 
basic scalar type string) : 4092 
 4093 
myGeoValueDomain  
Code Meaning 
AF Afghanistan 
BS Bahamas 
FJ Fiji 
GA Gabon 
KH Cambodia 
117 
 
MO Macao 
PK Pakistan 
QA Quatar 
UG Uganda 
 4094 
 4095 
Example 3 (on external Value Domain):   4096 
 4097 
DS_r := DS_1#Id_2  in  myGeoValueDomain     results in:  4098 
 4099 
DS_r 
Id_1 Id_2 bool_var 
2012 BS TRUE 
2012 GZ FALSE 
2012 SQ FALSE 
2012 MO TRUE 
2012 FJ TRUE 
2012 CQ FALSE 
 4100 
 4101 
match_characters   match_characters 4102 
 4103 
Syntax 4104 
  4105 
match_characters ( op , pattern ) 4106 
 4107 
Input parameters 4108 
op the dataset to be checked 4109 
pattern the regular expression to check the Data Set or the Component against 4110 
 4111 
Examples of valid syntaxes 4112 
 4113 
match_characters(ds1, “[abc]+\d\d”) 4114 
ds1 [ calc m1 := match_characters(ds1, “[abc]+\d\d”) ] 4115 
 4116 
Semantics for scalar operations 4117 
match_characters returns TRUE if op matches the regular expression regexp, FALSE otherwise. The 4118 
string regexp is an Extended Regular Expression as described in the POSIX standard. Different 4119 
implementations of VTL may implement different versions of the POSIX standard therefore it is 4120 
possible that match_characters may behave in slightly different ways.  4121 
 4122 
Input parameters type 4123 
 4124 
op :: dataset   {measure<string> _} 4125 
|  component<string> 4126 
|  string 4127 
pattern  :: string | component<string> 4128 
 4129 
 4130 
Result type 4131 
result ::   dataset   {  measure<booelan>  bool_var  } 4132 
118 
 
|   component<boolean> 4133 
|   boolean    4134 
 4135 
Additional constraints 4136 
If op is a Data Set then it has exactly one measure. 4137 
pattern is a POSIX regular expression. 4138 
  4139 
Behaviour 4140 
The operator has the typical behaviour of the “Operators changing the data type” (see the section “Typical 4141 
behaviours of the ML Operators”).   4142 
 4143 
Examples 4144 
Given the following Dataset DS_1: 4145 
DS_1 
Id_1 Id_2 Id_3 Id_4 Me_1 
G Total Percentage Total AX123 
R Total Percentage Total AX2J5 
 4146 
 4147 
DS_r:=(ds1, “[:alpha:]{2}[:digit:]{3}”)  results in: 4148 
 4149 
DS_r 
Id_1 Id_2 Id_3 Id_4 bool_var 
G Total Percentage Total TRUE 
R Total Percentage Total FALSE 
 4150 
 4151 
Isnull:   isnull 4152 
Syntax 4153 
isnull ( op ) 4154 
 4155 
Input parameters 4156 
operand mandatory the operand  4157 
 4158 
Examples of valid syntaxes 4159 
isnull(DS_1) 4160 
 4161 
Semantics for scalar operations 4162 
The operator returns TRUE if the value of the operand is NULL, FALSE otherwise. 4163 
 4164 
Examples 4165 
isnull(“Hello”)   gives: FALSE 4166 
isnull(NULL)  gives: TRUE 4167 
 4168 
Input parameters type 4169 
op ::  dataset   {measure<scalar> _} 4170 
|  component<scalar> 4171 
|  scalar     4172 
 4173 
Result type 4174 
result ::   dataset   {  measure<boolean>  bool_var  } 4175 
|   component<boolean> 4176 
|   boolean    4177 
119 
 
 4178 
Additional constraints 4179 
If op is a Data Set then it has exactly one measure. 4180 
  4181 
Behaviour 4182 
The operator has the typical behaviour of the “Operators changing the data type” (see the section “Typical 4183 
behaviours of the ML Operators”).   4184 
 4185 
Examples 4186 
Given the operand Data Set DS_1:   4187 
 4188 
DS_1 
Id_1 Id_2 Id_3 Id_4 Me_1 
2012 B Total Total 11094850 
2012 G Total Total 11123034 
2012 S Total Total NULL 
2012 M Total Total 417546 
2012 F Total Total 5401267 
2012 N Total Total NULL 
 4189 
Example 1: DS_r := isnull(DS_1)  results in: 4190 
 4191 
DS_r 
Id_1 Id_2 Id_3 Id_4 bool_var 
2012 B Total Total FALSE 
2012 G Total Total FALSE 
2012 S Total Total TRUE 
2012 M Total Total FALSE 
2012 F Total Total FALSE 
2012 N Total Total TRUE 
 4192 
Example 2 (on Components): DS_r := DS_1[ Me_2 := is_null(Me_1) ]  results in: 4193 
 4194 
DS_r 
Id_1 Id_2 Id_3 Id_4 Me_1 Me_2 
2012 B Total Total 11094850 FALSE 
2012 G Total Total 11123034 FALSE 
2012 S Total Total NULL TRUE 
2012 M Total Total 417546 FALSE 
2012 F Total Total 5401267 FALSE 
2012 N Total Total NULL TRUE 
 4195 
 4196 
120 
 
Exists in :  exists_in    4197 
 4198 
Syntax 4199 
exists_in ( op1, op2 { , retain } ) 4200 
 4201 
retain ::= true | false | all 4202 
 4203 
Input parameters 4204 
op1  the operand dataset 4205 
op2  the operand dataset 4206 
retain  the optional parameter to specify the Data Points to be returned (default: all) 4207 
 4208 
Examples of valid syntaxes 4209 
exists_in ( DS_1, DS_2, true ) 4210 
exists_in ( DS_1, DS_2 ) 4211 
exists_in ( DS_1, DS_2, all ) 4212 
 4213 
Semantics for scalar operations 4214 
This operator cannot be applied to scalar values. 4215 
 4216 
Input parameters type 4217 
op1,  4218 
op2 ::  dataset    4219 
 4220 
Result type 4221 
result ::   dataset   {  measure<boolean>  bool_var } 4222 
 4223 
Additional constraints 4224 
op2 has all the identifier components of op1.  4225 
 4226 
Behaviour 4227 
The operator checks if the combinations of values of the Identifiers existing in op1also exist in op2.  4228 
The result has the same Identifiers as op1 and a boolean Measure bool_var whose value, for each Data Point of 4229 
op1, is TRUE if the combination of values of the Identifier Components existing in op1 is found in a Data Point of 4230 
op2, FALSE otherwise. If retain is all then both the Data Points having bool_var = TRUE and bool_var = FALSE are 4231 
returned.  4232 
If retain is true then only the data points with bool_var = TRUE are returned. If retain is false then only the Data 4233 
Points with bool_var = FALSE are returned.If the retain parameter is omitted, the default is all. 4234 
The operator has the typical behaviour of the “Operators changing the data type” (see the section “Typical 4235 
behaviours of the ML Operators”).   4236 
 4237 
Examples 4238 
Given  the operand Data Sets DS_1 and DS_2: 4239 
 4240 
DS_1 
Id_1 Id_2 Id_3 Id_4 Me_1 
2012 B Total Total 11094850 
2012 G Total Total 11123034 
2012 S Total Total 46818219 
2012 M Total Total 417546 
2012 F Total Total 5401267 
2012 W Total Total 7954662 
 4241 
 4242 
 4243 
121 
 
DS_2 
Id_1 Id_2 Id_3 Id_4 Me_1 
2012 B Total Total 0.023 
2012 G Total M 0.286 
2012 S Total Total 0.064 
2012 M Total M 0.043 
2012 F Total Total NULL 
2012 W Total Total 0.08 
 4244 
Example 1:  DS_r := exists_in (DS_1, DS_2, all)   results in: 4245 
 4246 
DS_r 
Id_1 Id_2 Id_3 Id_4 bool_var 
2012 B Total Total TRUE 
2012 G Total Total FALSE 
2012 S Total Total TRUE 
2012 M Total Total FALSE 
2012 F Total Total TRUE 
2012 W Total Total TRUE 
 4247 
Example 2:  DS_r := exists_in (DS_1, DS_2, true)  results in: 4248 
 4249 
DS_r 
Id_1 Id_2 Id_3 Id_4 bool_var 
2012 B Total Total TRUE 
2012 S Total Total TRUE 
2012 F Total Total TRUE 
2012 W Total Total TRUE 
 4250 
Example 3:  DS_r := exists_in (DS_1, DS_2, false)  results in: 4251 
 4252 
DS_r 
Id_1 Id_2 Id_3 Id_4 bool_var 
2012 G Total Total FALSE 
2012 M Total Total FALSE 
 4253 
122 
 
VTL-ML  -  Boolean operators  4254 
Logical conjunction:  and 4255 
 4256 
Syntax 4257 
op1 and op2 4258 
 4259 
Input parameters 4260 
op1 the first operand  4261 
op2 the seconf operand  4262 
 4263 
Examples of valid syntaxes 4264 
DS_1 and DS_2 4265 
 4266 
Semantics for scalar operations 4267 
The and operator returns TRUE if both operands are TRUE, otherwise FALSE. The two operands must be of 4268 
boolean type.   4269 
For example: 4270 
FALSE and FALSE  gives FALSE 4271 
FALSE and TRUE    gives FALSE 4272 
TRUE  and FALSE  gives FALSE 4273 
TRUE  and TRUE    gives TRUE   4274 
 4275 
Input parameters type 4276 
op1, 4277 
op2 ::     dataset   {measure<boolean> _ } 4278 
|  component<boolean> 4279 
|  boolean     4280 
 4281 
Result type 4282 
result ::   dataset   {  measure<boolean>  _} 4283 
|   component<boolean> 4284 
|   boolean    4285 
 4286 
Additional constraints 4287 
None. 4288 
 4289 
Behaviour 4290 
The operator has the typical behaviour of the “Behaviour of Boolean operators” (see the section “Typical 4291 
behaviours of the ML Operators”).   4292 
  4293 
Examples 4294 
Given the operand Data Sets DS_1 and DS_2: 4295 
 4296 
DS_1 
Id_1 Id_2 Id_3 Id_4 Me_1 
M 15 B 2013 TRUE 
M 64 B 2013 FALSE 
M 65 B 2013 TRUE 
F 15 U 2013 FALSE 
F 64 U 2013 FALSE 
F 65 U 2013 TRUE 
123 
 
 4297 
 4298 
DS_2 
Id_1 Id_2 Id_3 Id_4 Me_1 
M 15 B 2013 FALSE 
M 64 B 2013 TRUE 
M 65 B 2013 TRUE 
F 15 U 2013 TRUE 
F 64 U 2013 FALSE 
F 65 U 2013 FALSE 
 4299 
 4300 
Example 1:  DS_r:= DS_1 and DS_2  results in: 4301 
 4302 
DS_r 
Id_1 Id_2 Id_3 Id_4 Me_1 
M 15 B 2013 FALSE 
M 64 B 2013 FALSE 
M 65 B 2013 TRUE 
F 15 U 2013 FALSE 
F 64 U 2013 FALSE 
F 65 U 2013 FALSE 
 4303 
Example 2 (on Components): DS_r := DS_1 [ Me_2:= Me_1 and true ]  results in: 4304 
 4305 
DS_r 
Id_1 Id_2 Id_3 Id_4 Me_1 Me_2 
M 15 B 2013 TRUE TRUE 
M 64 B 2013 FALSE FALSE 
M 65 B 2013 TRUE TRUE 
F 15 U 2013 FALSE FALSE 
F 64 U 2013 FALSE FALSE 
F 65 U 2013 TRUE TRUE 
Logical disjunction :  or 4306 
Syntax 4307 
op1  or  op2 4308 
 4309 
Input parameters 4310 
op1 the first operand  4311 
op2 the second operand  4312 
 4313 
Examples of valid syntaxes 4314 
DS_1 or DS_2 4315 
 4316 
Semantics for scalar operations 4317 
124 
 
The or operator returns TRUE if at least one of the operands is TRUE, otherwise FALSE. The two operands must 4318 
be of boolean type.  4319 
For example:  4320 
FALSE or FALSE gives FALSE 4321 
FALSE or TRUE  gives TRUE   4322 
TRUE  or FALSE gives TRUE   4323 
TRUE  or TRUE  gives TRUE   4324 
 4325 
Input parameters type 4326 
op1, 4327 
op2 ::     dataset   {measure<boolean> _ } 4328 
|  component<boolean> 4329 
|  boolean     4330 
Result type 4331 
result ::   dataset   {  measure<boolean> _ } 4332 
|   component<boolean> 4333 
|   boolean    4334 
 4335 
Additional constraints 4336 
None. 4337 
 4338 
Behaviour 4339 
The operator has the typical behaviour of the “Behaviour of Boolean operators” (see the section “Typical 4340 
behaviours of the ML Operators”).   4341 
 4342 
Examples 4343 
 Given the operand Data Sets DS_1 and DS_2:  4344 
 4345 
DS_1 
Id_1 Id_2 Id_3 Id_4 Me_1 
M 15 B 2013 TRUE 
M 64 B 2013 FALSE 
M 65 B 2013 TRUE 
F 15 U 2013 FALSE 
F 64 U 2013 FALSE 
F 65 U 2013 TRUE 
 4346 
 4347 
DS_2 
Id_1 Id_2 Id_3 Id_4 Me_1 
M 15 B 2013 FALSE 
M 64 B 2013 TRUE 
M 65 B 2013 TRUE 
F 15 U 2013 TRUE 
F 64 U 2013 FALSE 
F 65 U 2013 FALSE 
 4348 
Example 1: DS_r:= DS_1 or DS_2  results in: 4349 
 4350 
DS_r 
Id_1 Id_2 Id_3 Id_4 Me_1 
125 
 
M 15 B 2013 TRUE 
M 64 B 2013 TRUE 
M 65 B 2013 TRUE 
F 15 U 2013 TRUE 
F 64 U 2013 FALSE 
F 65 U 2013 TRUE 
 4351 
Example 2 (on Components): DS_r:= DS_1 [ Me_2:= Me_1 or true ]  results in: 4352 
 4353 
DS_r 
Id_1 Id_2 Id_3 Id_4 Me_1 Me_2 
M 15 B 2013 TRUE TRUE 
M 64 B 2013 FALSE TRUE 
M 65 B 2013 TRUE TRUE 
F 15 U 2013 FALSE TRUE 
F 64 U 2013 FALSE TRUE 
F 65 U 2013 TRUE TRUE 
 4354 
Exclusive disjunction :   xor 4355 
Syntax 4356 
op1  xor  op2 4357 
 4358 
Input parameters 4359 
op1 the first operand  4360 
op2 the second operand  4361 
 4362 
 4363 
Examples of valid syntaxes 4364 
DS_1  xor  DS_2 4365 
 4366 
Semantics for scalar operations 4367 
The xor operator returns TRUE if only one of the operand is TRUE (but not both), FALSE otherwise. The two 4368 
operands must be of boolean type.  4369 
For example: 4370 
FALSE xor  FALSE gives FALSE 4371 
FALSE xor  TRUE   gives TRUE   4372 
TRUE  xor  FALSE gives TRUE   4373 
TRUE  xor  TRUE   gives FALSE 4374 
 4375 
Input parameters type 4376 
op1, 4377 
op2 ::     dataset   {measure<boolean> _  } 4378 
|  component<boolean> 4379 
|  boolean     4380 
 4381 
Result type 4382 
result ::   dataset   {  measure<boolean>  _  } 4383 
|   component<boolean> 4384 
|   boolean    4385 
 4386 
126 
 
Additional constraints 4387 
None. 4388 
  4389 
Behaviour 4390 
The operator has the typical behaviour of the “Behaviour of Boolean operators” (see the section “Typical 4391 
behaviours of the ML Operators”).   4392 
 4393 
Examples 4394 
Given the operand Data Sets DS_1 and DS_2:  4395 
 4396 
DS_1 
Id_1 Id_2 Id_3 Id_4 Me_1 
M 15 B 2013 TRUE 
M 64 B 2013 FALSE 
M 65 B 2013 TRUE 
F 15 U 2013 FALSE 
F 64 U 2013 FALSE 
F 65 U 2013 trTRUEue 
 4397 
 4398 
DS_2 
Id_1 Id_2 Id_3 Id_4 Me_1 
M 15 B 2013 FALSE 
M 64 B 2013 TRUE 
M 65 B 2013 TRUE 
F 15 U 2013 TRUE 
F 64 U 2013 FALSE 
F 65 U 2013 FALSE 
 4399 
Example 1: DS_r:=DS_1 xor DS_2  results in: 4400 
 4401 
DS_r 
Id_1 Id_2 Id_3 Id_4 Me_1 
M 15 B 2013 TRUE 
M 64 B 2013 TRUE 
M 65 B 2013 FALSE 
F 15 U 2013 TRUE 
F 64 U 2013 FALSE 
F 65 U 2013 TRUE 
 4402 
Example 2 (on Components): DS_r:= DS_1 [ Me_2:= Me_1  xor  true ]  results in: 4403 
 4404 
DS_r 
Id_1 Id_2 Id_3 Id_4 Me_1 Me_2 
M 15 B 2013 TRUE FALSE 
M 64 B 2013 FALSE TRUE 
127 
 
M 65 B 2013 TRUE FALSE 
F 15 U 2013 FALSE TRUE 
F 64 U 2013 FALSE TRUE 
F 65 U 2013 TRUE FALSE 
 4405 
Logical negation :   not 4406 
 4407 
Syntax 4408 
not  op 4409 
 4410 
Input parameters 4411 
op  the operand  4412 
 4413 
Examples of valid syntaxes 4414 
not  DS_1 4415 
 4416 
Semantics for scalar operations 4417 
The not operator returns TRUE if op is FALSE, otherwise TRUE. The input operand must be of boolean type.  4418 
For example: 4419 
not  FALSE gives  TRUE   4420 
not  TRUE   gives  FALSE 4421 
 4422 
Input parameters type 4423 
op ::  dataset   {measure<boolean> _  } 4424 
|  component<boolean> 4425 
|  boolean     4426 
 4427 
Result type 4428 
result ::   dataset   {  measure<boolean>  _  } 4429 
|   component<boolean> 4430 
|   boolean    4431 
 4432 
Additional constraints 4433 
None. 4434 
  4435 
Behaviour 4436 
The operator has the typical behaviour of the “Behaviour of Boolean operators” (see the section “Typical 4437 
behaviours of the ML Operators”).   4438 
 4439 
Examples 4440 
Given the operand Data Set DS_1: 4441 
 4442 
DS_1 
Id_1 Id_2 Id_3 Id_4 Me_1 
M 15 B 2013 TRUE 
M 64 B 2013 FALSE 
M 65 B 2013 TRUE 
F 15 U 2013 FALSE 
F 64 U 2013 FALSE 
F 65 U 2013 TRUE 
 4443 
128 
 
Example 1: DS_r:= not DS_1  results in: 4444 
 4445 
DS_r 
Id_1 Id_2 Id_3 Id_4 Me_1 
M 15 B 2013 FALSE 
M 64 B 2013 TRUE 
M 65 B 2013 FALSE 
F 15 U 2013 TRUE 
F 64 U 2013 TRUE 
F 65 U 2013 false 
 4446 
Example 2 (on Components): DS_r:= DS_1 [ calc Me_2 := not Me_1 ]  results in: 4447 
 4448 
DS_r 
Id_1 Id_2 Id_3 Id_4 Me_1 Me_2 
M 15 B 2013 TRUE FALSE 
M 64 B 2013 FALSE TRUE 
M 65 B 2013 TRUE FALSE 
F 15 U 2013 FALSE TRUE 
F 64 U 2013 FALSE TRUE 
F 65 U 2013 TRUE FALSE 
 4449 
129 
 
VTL-ML  -  Time operators 4450 
This chapter describes the time operators, which are the operators dealing with time, date and time_period 4451 
basic scalar types. The general aspects of the behaviour of these operators is described in the section “Behaviour 4452 
of the Time Operators”. 4453 
The time data type is the most general type and denotes a generic time interval, having  start and end points in 4454 
time and therefore a duration, which is the time intervening between the start and end points. The date data type 4455 
denotes a generic time instant (a point in time), which is a time interval with zero duration. The time_period data 4456 
type denotes a regular time interval whose regular duration is explicitly represented inside each time_period 4457 
value and is named period_indicator. In some sense, we say that date and time_period are special cases of time, 4458 
the former with coinciding extremes and zero duration and the latter with regular duration. The time data type is 4459 
overarching in the sense that it comprises date and time_period. Finally, duration data type represents a generic 4460 
time span, independently of any specific start and end date. 4461 
The time, date and time period formats used here are explained in the User Manual in the section “External 4462 
representations and literals used in the VTL Manuals”.  4463 
The period indicator P id of the duration type and its possible values are:  4464 
  D  Day 4465 
  W  Week 4466 
  M  Month 4467 
  Q  Quarter  4468 
  S  Semester 4469 
  A  Year 4470 
 4471 
As already said, these representation are not prescribed by VTL and are not part of the VTL standard, each VTL system 4472 
can personalize the representation of time, date, time_period and duration as desired. The formats shown above are only 4473 
the ones used in the examples. 4474 
For a fully-detailed explanation, please refer to the User Manual. 4475 
 4476 
Period indicator :  period_indicator 4477 
 4478 
The operator period_indicator extracts the period indicator from a time_period value.  4479 
Syntax 4480 
period_indicator  ( { op } ) 4481 
 4482 
Input parameters 4483 
op the operand  4484 
 4485 
Examples of valid syntaxes   4486 
period_indicator ( ds_1 ) 4487 
period_indicator       (if used in a clause the operand op can be omitted)  4488 
 4489 
Semantics for scalar operations 4490 
period_indicator returns the period indicator of a time_period value. The period indicator is the part of the 4491 
time_period value which denotes the duration of the time period (e.g. day, week, month …).    4492 
 4493 
Input parameters type 4494 
op :: dataset { identifier <time_period> _  , identifier _* } 4495 
 | component<time_period> 4496 
 | time_period 4497 
 4498 
Result type 4499 
result ::   dataset { measure<duration> duration_var  } 4500 
  | component <duration> 4501 
  | duration 4502 
 4503 
130 
 
Additional constraints 4504 
If op is a Data Set then it has exactly an Identifier of type time_period and may have other Identifiers. If the 4505 
operator is used in a clause and op is omitted, then the Data Set to which the clause is applied has exactly an 4506 
Identifier of type time_period. 4507 
 4508 
Behaviour 4509 
The operator extracts the period indicator part of the time_period value. The period indicator is computed for 4510 
each Data Point.  When the operator is used in a clause, it extracts the period indicator from the time_period 4511 
value the Data Set to which the clause is applied. 4512 
The operator returns a Data Set with the same Identifiers of op and one Measure of type duration named 4513 
duration_var.  As for all the Variables, a proper Value Domain must be defined to contain the possible values of 4514 
the period indicator and duration_var. The values used in the examples are listed at the beginning of this chapter 4515 
"VTL-ML Time operators".  4516 
Examples 4517 
Given the Data Set DS_1: 4518 
DS_r 
Id_1 Id_2 Id_3 Me_1 
A 1 2010 10 
A 1 2013Q1 50 
 4519 
Example 1: DS_r := period_indicator ( DS_1 ) results in: 4520 
 4521 
DS_r 
Id_1 Id_2 Id_3 duration_var 
A 1 2010 A 
A 1 2013Q1 Q 
 4522 
Example 2 (on component):  DS_r := DS_1 [ filter period_indicator ( Id_3 ) = “A" ] results in: 4523 
 4524 
DS_r 
Id_1 Id_2 Id_3 Me_1 
A 1 2010 10 
 4525 
 4526 
 4527 
Fill time series : fill_time_series 4528 
 4529 
Syntax 4530 
fill_time_series  ( op { , limitsMethod } ) 4531 
 4532 
limitsMethod ::= single | all 4533 
 4534 
Input parameters 4535 
op the operand  4536 
limitsMethod method for determining the limits of the time interval to be filled (default: all) 4537 
 4538 
Examples of valid syntaxes  4539 
fill_time_series ( ds ) 4540 
fill_time_series ( ds, all ) 4541 
131 
 
 4542 
Semantics for scalar operations 4543 
The fill_time_series operator does not perform scalar operations. 4544 
 4545 
Input parameters type: 4546 
op :: dataset { identifier <time > _ , identifier _* } 4547 
 4548 
Result type: 4549 
result :: dataset { identifier <time > _ , identifier _* } 4550 
 4551 
 4552 
Additional constraints 4553 
The operand op has an Identifier of type time, date or time_period and may have other Identifiers. 4554 
 4555 
Behaviour 4556 
This operator can be applied only on Data Sets of time series and returns a Data Set of time series. 4557 
The operator fills the possibly missing Data Points of all the time series belonging to the operand op within the 4558 
time limits automatically determined by applying the limit_method.  4559 
If limitsMmethod is all, the time limits are determined with reference to all the time_series of the Data Set: the 4560 
limits are the minimum and the maximum values of the reference time Identifier Component of the Data Set.   4561 
If limitsMmethod is single, the time limits are determined with reference to each single time_series of the Data 4562 
Set: the limits are the minimum and the maximum values of the reference time Identifier Component of the time 4563 
series. 4564 
The expected Data Points are determined, for each  time series, by considering the limits above and the period 4565 
(frequency) of the time series: all the Identifiers are kept unchanged except the reference time Identifier, which is 4566 
increased of one period at a time (e.g. day, week, month, quarter, year) from the lower to the upper time limit.  4567 
For each increase, an expected Data Point is identified.  4568 
If this expected Data Points is missing, it is added to the Data Set. For the added Data Points, Measures and 4569 
Attributes assume the NULL value.  4570 
The output Data Set has the same Identifier, Measure and Attribute Components as the operand Data Set. The 4571 
ouput Data Set contains the same time series as the operand, because the time series Identifiers (all the 4572 
Identifiers except the reference time Identifier) are not changed. 4573 
As mentioned in the section “Behaviour of the Time Operators”, the operator is assumed to know which is the 4574 
reference time Identifier as well as the period of each time series. 4575 
 4576 
Examples 4577 
Given the Data Set DS_1, which contains yearly time series, where Id_2 is the reference time Identifier of  time 4578 
type: 4579 
 4580 
DS_1 
Id_1 Id_2 Me_1 
A 2010-01/2010-12 "hello world" 
A 2012-01/2012-12 "say hello" 
A 2013-01/2013-12 "he" 
B 2011-01/2011-12 "hi, hello! " 
B 2012-01/2012-12 "hi” 
B 2014-01/2014-12 “hello!” 
 4581 
Example 1:   DS_r := fill_time_series ( DS_1, single )  results in: 4582 
 4583 
DS_r 
Id_1 Id_2 Me_1 
A 2010-01/2010-12 "hello world" 
132 
 
A 2011-01/2011-12 NULL 
A 2012-01/2012-12 "say hello" 
A 2013-01/2013-12 "he" 
B 2011-01/2011-12 "hi, hello! " 
B 2012-01/2012-12 "hi” 
B 2013-01/2013-12 NULL 
B 2014-01/2014-12 “hello!” 
 4584 
Example 2:   DS_r := fill_time_series ( DS_1, all )  results in: 4585 
 4586 
DS_r 
Id_1 Id_2 Me_1 
A 2010-01/2010-12 "hello world" 
A 2011-01/2011-12 NULL 
A 2012-01/2012-12 "say hello" 
A 2013-01/2013-12 "he" 
A 2014-01/2014-12 NULL 
B 2010-01/2010-12 NULL 
B 2011-01/2011-12 "hi, hello! " 
B 2012-01/2012-12 "hi” 
B 2013-01/2013-12 NULL 
B 2014-01/2014-12 “hello!” 
 4587 
Given the Data Set DS_2, which contains yearly time series, where Id_2 is the reference time Identifier of date 4588 
type and conventionally each period is identified by its last day: 4589 
 4590 
DS_2 
Id_1 Id_2 Me_1 
A 2010-12-31 "hello world" 
A 2012-12-31 "say hello" 
A 2013-12-31 "he" 
B 2011-12-31 "hi, hello! " 
B 2012-12-31 "hi” 
B 2014-12-31 “hello!” 
 4591 
Example 3:   DS_r := fill_time_series ( DS_2, single )  results in: 4592 
 4593 
DS_r 
Id_1 Id_2 Me_1 
A 2010-12-31 "hello world" 
A 2011-12-31 NULL 
A 2012-12-31 "say hello" 
A 2013-12-31 "he" 
B 2011-12-31 "hi, hello! " 
133 
 
B 2012-12-31 "hi” 
B 2013-12-31 NULL 
B 2014-12-31 “hello!” 
 4594 
Example 4:   DS_r := fill_time_series ( DS_2, all )   results in: 4595 
 4596 
DS_r 
Id_1 Id_2 Me_1 
A 2010-12-31 "hello world" 
A 2011-12-31 NULL 
A 2012-12-31 "say hello" 
A 2013-12-31 "he" 
A 2014-12-31 NULL 
B 2010-12-31 NULL 
B 2011-12-31 "hi, hello! " 
B 2012-12-31 "hi” 
B 2013-12-31 NULL 
B 2014-12-31 “hello!” 
 4597 
 4598 
Given the Data Set DS_3, which contains yearly time series, where Id_2 is the reference time Identifier of  4599 
time_period type: 4600 
 4601 
DS_3 
Id_1 Id_2 Me_1 
A 2010Y "hello world" 
A 2012Y "say hello" 
A 2013Y "he" 
B 2011Y "hi, hello! " 
B 2012Y "hi” 
B 2014Y “hello!” 
 4602 
Example 5:   DS_r := fill_time_series ( DS_3, single )  results in: 4603 
 4604 
DS_r 
Id_1 Id_2 Me_1 
A 2010Y "hello world" 
A 2011Y NULL 
A 2012Y "say hello" 
A 2013Y "he" 
B 2011Y "hi, hello! " 
B 2012Y "hi” 
B 2013Y NULL 
B 2014Y “hello!” 
134 
 
 4605 
Example 6:   DS_r := fill_time_series ( DS_3, all )   results in: 4606 
 4607 
DS_r 
Id_1 Id_2 Me_1 
A 2010Y "hello world" 
A 2011Y NULL 
A 2012Y "say hello" 
A 2013Y "he" 
A 2014Y NULL 
B 2010Y NULL 
B 2011Y "hi, hello! " 
B 2012Y "hi” 
B 2013Y NULL 
B 2014Y “hello!” 
 4608 
 4609 
Given the Data Set DS_4, which contains both quarterly and annual time series relevant to the same 4610 
phenomenon “A”, where Id_2 is the reference time Identifier of  time_period type,: 4611 
 4612 
DS_4 
Id_1 Id_2 Me_1 
A 2010Y "hello world" 
A 2012Y "say hello" 
A 2010Q1 “he” 
A 2010Q2 "hi, hello! " 
A 2010Q4 "hi” 
A 2011Q2 “hello!” 
 4613 
Example 7:   DS_r := fill_time_series ( DS_4, single )  results in: 4614 
 4615 
DS_r 
Id_1 Id_2 Me_1 
A 2010Y "hello world" 
A 2011Y NULL 
A 2012Y "say hello" 
A 2010Q1 “he” 
A 2010Q2 "hi, hello! " 
A 2010Q3 NULL 
A 2010Q4 "hi” 
A 2011Q2 “hello!” 
 4616 
Example 8:   DS_r := fill_time_series ( DS_4, all )   results in: 4617 
 4618 
DS_r 
Id_1 
Id_2 
A 
2010Y 
Me_1 
"hello world" 
A 
2011Y 
NULL 
A 
2012Y 
"say hello" 
A 
2010Q1 
“he” 
A 
2010Q2 
"hi, hello! " 
A 
2010Q3 
NULL 
A 
2010Q4 
"hi” 
A 
2011Q1 
NULL 
A 
2011Q2 
“hello!” 
A 
2011Q3 
NULL 
A 
2011Q4 
NULL 
A 
2012Q1 
NULL 
A 
2012Q2 
NULL 
A 
2012Q3 
NULL 
A 
2012Q4 
NULL 
4619 
135 
136 
 
 4620 
Flow to stock : flow_to_stock 4621 
 4622 
Syntax 4623 
flow_to_stock  ( op ) 4624 
 4625 
Input Parameters 4626 
op  the operand  4627 
 4628 
Examples of valid syntaxes  4629 
flow_to_stock ( ds_1 ) 4630 
 4631 
Semantics for scalar operations 4632 
This operator does not perform scalar operations. 4633 
 4634 
Input parameters type: 4635 
op :: dataset { identifier < time > _ ,  identifier _* , measure<number>   _+  }   4636 
 4637 
Result type: 4638 
result :: dataset { identifier < time > _ ,  identifier _* , measure<number>   _+  }   4639 
 4640 
Additional constraints 4641 
The operand dataset has an Identifier of type time, date or time_period and may have other Identifiers. 4642 
 4643 
Behaviour 4644 
The statistical data that describe the “state” of a phenomenon on a given moment (e.g. resident population on a 4645 
given moment) are often referred to as “stock data”.   4646 
On the contrary, the statistical data that describe “events” which can happen continuously (e.g. changes in the 4647 
resident population, such as births, deaths, immigration, emigration), are often referred to as “flow data”.  4648 
This operator takes in input a Data Set which are interpreted as flows and calculates the change of the 4649 
corresponding stock since the beginning of each time series by summing the relevant flows. In other words, the 4650 
operator perform the cumulative sum from the first Data Point of each time series to each other following Data 4651 
Point of the same time series. 4652 
The flow_to_stock operator can be applied only on Data Sets of time series and returns a Data Set of time series. 4653 
The result Data Set has the same Identifier, Measure and Attribute Components as the operand Data Set and 4654 
contains the same time series as the operand, because the time series Identifiers (all the Identifiers except the 4655 
reference time Identifier) are not changed. 4656 
As mentioned in the section “Behaviour of the Time Operators”, the operator is assumed to know which is the 4657 
time Identifier as well as the period of each time series. 4658 
 4659 
 4660 
Examples 4661 
 4662 
Given the Data Set DS_1, which contains yearly time series, where Id_2 is the reference time Identifier of  time 4663 
type: 4664 
 4665 
DS_1 
Id_1 Id_2 Me_1 
A 2010-01/2010-12 2 
A 2011-01/2011-12 5 
A 2012-01/2012-12 -3 
A 2013-01/2013-12 9 
B 2010-01/2010-12 4 
137 
 
B 2011-01/2011-12 -8 
B 2012-01/2012-12 0 
B 2013-01/2013-12 6 
 4666 
Example 1:   DS_r := flow_to_stock ( DS_1 )  results in: 4667 
 4668 
DS_r 
Id_1 Id_2 Me_1 
A 2010-01/2010-12 2 
A 2011-01/2011-12 7 
A 2012-01/2012-12 4 
A 2013-01/2013-12 13 
B 2010-01/2010-12 4 
B 2011-01/2011-12 -4 
B 2012-01/2012-12 -4 
B 2013-01/2013-12 2 
 4669 
 4670 
Given the Data Set DS_2, which contains yearly time series, where Id_2 is the reference time Identifier of date 4671 
type (conventionally each period is identified by its last day): 4672 
 4673 
DS_2 
Id_1 Id_2 Me_1 
A 2010-12-31 2 
A 2011-12-31 5 
A 2012-12-31 -3 
A 2013-12-31 9 
B 2010-12-31 4 
B 2011-12-31 -8 
B 2012-12-31 0 
B 2013-12-31 6 
 4674 
Example 2:   DS_r := flow_to_stock ( DS_2 )  results in: 4675 
 4676 
DS_r 
Id_1 Id_2 Me_1 
A 2010-12-31 2 
A 2011-12-31 7 
A 2012-12-31 4 
A 2013-12-31 13 
B 2010-12-31 4 
B 2011-12-31 -4 
B 2012-12-31 -4 
B 2013-12-31 2 
138 
 
 4677 
Given the Data Set DS_3, which contains yearly time series, where Id_2 is the reference time Identifier of  4678 
time_period type: 4679 
 4680 
DS_3 
Id_1 Id_2 Me_1 
A 2010Y 2 
A 2011Y 5 
A 2012Y -3 
A 2013Y 9 
B 2010Y 4 
B 2011Y -8 
B 2012Y 0 
B 2013Y 6 
 4681 
Example 3:   DS_r := flow_to_stock ( DS_3 )  results in: 4682 
 4683 
DS_r 
Id_1 Id_2 Me_1 
A 2010Y 2 
A 2011Y 7 
A 2012Y 4 
A 2013Y 13 
B 2010Y 4 
B 2011Y -4 
B 2012Y -4 
B 2013Y 2 
 4684 
 4685 
Given the Data Set DS_4, which contains both quarterly and annual time series relevant to the same 4686 
phenomenon “A”, where Id_2 is the reference time Identifier of time_period type: 4687 
 4688 
DS_4 
Id_1 Id_2 Me_1 
A 2010Y 2 
A 2011Y 7 
A 2012Y 4 
A 2013Y 13 
A 2010Q1 2 
A 2010Q2 -3 
A 2010Q3 7 
A 2010Q4 -4 
 4689 
Example 4:   DS_r := flow_to_stock ( DS_3 )  results in: 4690 
 4691 
139 
 
DS_r 
Id_1 Id_2 Me_1 
A 2010Y 2 
A 2011Y 9 
A 2012Y 13 
A 2013Y 26 
A 2010Q1 2 
A 2010Q2 -1 
A 2010Q3 6 
A 2010Q4 2 
 4692 
 4693 
Stock to flow :  stock_to_flow 4694 
 4695 
Syntax 4696 
stock_to_flow  ( op ) 4697 
 4698 
Input parameters 4699 
  4700 
op  the operand 4701 
 4702 
Examples of valid syntaxes  4703 
stock_to_flow ( ds_1 ) 4704 
 4705 
Semantics for scalar operations 4706 
This operator does not perform scalar operations. 4707 
 4708 
Input parameters type: 4709 
op :: dataset { identifier < time > _ , identifier _* , measure<number>   _+  }  4710 
 4711 
Result type: 4712 
result :: dataset { identifier < time > _ ,  identifier _* , measure<number>   _+  }  4713 
 4714 
Additional constraints 4715 
The operand dataset has an Identifier of type time, date or time_period and may have other Identifiers. 4716 
 4717 
Behaviour 4718 
The statistical data that describe the “state” of a phenomenon on a given moment (e.g. resident population on a 4719 
given moment) are often referred to as “stock data”.   4720 
On the contrary, the statistical data that describe “events” which can happen continuously (e.g. changes in the 4721 
resident population, such as births, deaths, immigration, emigration), are often referred to as “flow data”.  4722 
This operator takes in input a Data Set of time series which is interpreted as stock data and, for each time series, 4723 
calculates the corresponding flow data by subtracting from the measure values of each regular period the 4724 
corresponding measure values of the previous one. 4725 
The stock_to_flow operator can be applied only on Data Sets of time series and returns a Data Set of time series. 4726 
The result Data Set has the same Identifier, Measure and Attribute Components as the operand Data Set and 4727 
contains the same time series as the operand, because the time series Identifiers (all the Identifiers except the 4728 
reference time Identifier) are not changed. 4729 
The Attribute propagation rule is not applied. 4730 
As mentioned in the section “Behaviour of the Time Operators”, the operator is assumed to know which is the 4731 
time Identifier as well as the period of each time series. 4732 
 4733 
140 
 
 4734 
Examples 4735 
 4736 
Given the Data Set DS_1, which contains yearly time series, where Id_2 is the reference time Identifier of  time 4737 
type: 4738 
 4739 
DS_1 
Id_1 Id_2 Me_1 
A 2010-01/2010-12 2 
A 2011-01/2011-12 7 
A 2012-01/2012-12 4 
A 2013-01/2013-12 13 
B 2010-01/2010-12 4 
B 2011-01/2011-12 -4 
B 2012-01/2012-12 -4 
B 2013-01/2013-12 2 
 4740 
Example 1:   DS_r := stock_to_flow ( DS_1 )  results in: 4741 
 4742 
DS_r 
Id_1 Id_2 Me_1 
A 2010-01/2010-12 2 
A 2011-01/2011-12 5 
A 2012-01/2012-12 -3 
A 2013-01/2013-12 9 
B 2010-01/2010-12 4 
B 2011-01/2011-12 -8 
B 2012-01/2012-12 0 
B 2013-01/2013-12 6 
 4743 
 4744 
Given the Data Set DS_2, which contains yearly time series, where Id_2 is the reference time Identifier of  date 4745 
type (conventionally each period is identified by its last day): 4746 
 4747 
DS_2 
Id_1 Id_2 Me_1 
A 2010-12-31 2 
A 2011-12-31 7 
A 2012-12-31 4 
A 2013-12-31 13 
B 2010-12-31 4 
B 2011-12-31 -4 
B 2012-12-31 -4 
B 2013-12-31 2 
 4748 
Example 2:   DS_r := stock_to_flow ( DS_2 )  results in: 4749 
141 
 
 4750 
DS_r 
Id_1 Id_2 Me_1 
A 2010-12-31 2 
A 2011-12-31 5 
A 2012-12-31 -3 
A 2013-12-31 9 
B 2010-12-31 4 
B 2011-12-31 -8 
B 2012-12-31 0 
B 2013-12-31 6 
 4751 
 4752 
Given the Data Set DS_3, which contains yearly time series, where Id_2 is the reference time Identifier of 4753 
time_period type: 4754 
 4755 
DS_3 
Id_1 Id_2 Me_1 
A 2010Y 2 
A 2011Y 7 
A 2012Y 4 
A 2013Y 13 
B 2010Y 4 
B 2011Y -4 
B 2012Y -4 
B 2013Y 2 
 4756 
Example 3:   DS_r := stock_to_flow ( DS_3 )  results in: 4757 
 4758 
DS_r 
Id_1 Id_2 Me_1 
A 2010Y 2 
A 2011Y 5 
A 2012Y -3 
A 2013Y 9 
B 2010Y 4 
B 2011Y -8 
B 2012Y 0 
B 2013Y 6 
 4759 
 4760 
 4761 
Given the Data Set DS_4, which contains both quarterly and annual time series relevant to the same 4762 
phenomenon “A”, where Id_2 is the time Identifier of time_period type: 4763 
 4764 
142 
 
DS_4 
Id_1 Id_2 Me_1 
A 2010Y 2 
A 2011Y 9 
A 2012Y 13 
A 2013Y 26 
A 2010Q1 2 
A 2010Q2 -1 
A 2010Q3 6 
A 2010Q4 2 
 4765 
Example 4:  DS_r := stock_to_flow ( DS_4 )  results in: 4766 
 4767 
DS_r 
Id_1 Id_2 Me_1 
A 2010Y 2 
A 2011Y 7 
A 2012Y 4 
A 2013Y 13 
A 2010Q1 2 
A 2010Q2 -3 
A 2010Q3 7 
A 2010Q4 -4 
 4768 
Time shift : timeshift 4769 
Syntax 4770 
timeshift  ( op ,  shiftNumber  ) 4771 
 4772 
Input parameters 4773 
op the operand  4774 
shiftNumber the number of periods to be shifted 4775 
 4776 
Examples of valid syntaxes  4777 
timeshift ( DS_1,  2 )  4778 
timeshift ( DS_1 ) 4779 
 4780 
Semantics for scalar operations 4781 
This operator does not perform scalar operations. 4782 
 4783 
Input parameters type: 4784 
op ::  dataset { identifier < time > _ , identifier _* } 4785 
shiftNumber ::  integer   4786 
 4787 
Result type: 4788 
result :: dataset { identifier < time > _ , identifier _* } 4789 
 4790 
Additional constraints 4791 
The operand dataset has an Identifier of type time,  date or time_period and may have other Identifiers. 4792 
143 
 
. 4793 
 4794 
Behaviour 4795 
This operator takes in input a Data Set of time series and, for each time series of the Data Set, shifts the reference 4796 
time Identifier of a number of periods (of the time series) equal to the shift_number parameter.  If shift_number 4797 
is negative, the shift is in the past, otherwise in the future.  For example, if the period of the time series is month 4798 
and shift_number is -1 the reference time Identifier is shifted of two months in the past. 4799 
The operator can be applied only on Data Sets of time series and returns a Data Set of time series. 4800 
The result Data Set has the same Identifier, Measure and Attribute Components as the operand Data Set and 4801 
contains the same time series as the operand, because the time series Identifiers (all the Identifiers except the 4802 
reference time Identifier) are not changed. 4803 
The Attribute propagation rule is not applied. 4804 
As mentioned in the section “Behaviour of the Time Operators”, the operator is assumed to know which is the 4805 
time Identifier as well as the period of each data point. 4806 
 4807 
Examples 4808 
Given the Data Set DS_1, which contains yearly time series, where Id_2 is the reference time Identifier of time 4809 
type: 4810 
 4811 
DS_1 
Id_1 Id_2 Me_1 
A 2010-01/2010-12 "hello world" 
A 2011-01/2011-12 NULL 
A 2012-01/2012-12 "say hello" 
A 2013-01/2013-12 "he" 
B 2010-01/2010-12 "hi, hello! " 
B 2011-01/2011-12 "hi” 
B 2012-01/2012-12 NULL 
B 2013-01/2013-12 “hello!” 
 4812 
Example 1:   DS_r := time_shift ( DS_1 , -1  )  results in: 4813 
 4814 
DS_r 
Id_1 Id_2 Me_1 
A 2009-01/2009-12 "hello world" 
A 2010-01/2010-12 NULL 
A 2011-01/2011-12 "say hello" 
A 2012-01/2012-12 "he" 
B 2009-01/2009-12 "hi, hello! " 
B 2010-01/2010-12 "hi” 
B 2011-01/2011-12 NULL 
B 2012-01/2012-12 “hello!” 
 4815 
 4816 
Given the Data Set DS_2, which contains yearly time series, where Id_2 is the reference time Identifier of date 4817 
type (conventionally each period is identified by its last day): 4818 
 4819 
144 
 
DS_2 
Id_1 Id_2 Me_1 
A 2010-12-31 "hello world" 
A 2011-12-31 NULL 
A 2012-12-31 "say hello" 
A 2013-12-31 "he" 
B 2010-12-31 "hi, hello! " 
B 2011-12-31 "hi” 
B 2012-12-31 NULL 
B 2013-12-31 “hello!” 
 4820 
Example 2:  DS_r := time_shift ( DS_2 , 2  )  results in: 4821 
 4822 
DS_r 
Id_1 Id_2 Me_1 
A 2012-12-31 "hello world" 
A 2013-12-31 NULL 
A 2014-12-31 "say hello" 
A 2015-12-31 "he" 
B 2012-12-31 "hi, hello! " 
B 2013-12-31 "hi” 
B 2014-12-31 NULL 
B 2015-12-31 “hello!” 
 4823 
 4824 
Given the Data Set DS_3, which contains yearly time series, where Id_2 is the reference time Identifier of 4825 
time_period type: 4826 
 4827 
DS_3 
Id_1 Id_2 Me_1 
A 2010Y "hello world" 
A 2011Y NULL 
A 2012Y "say hello" 
A 2013Y "he" 
B 2010Y "hi, hello! " 
B 2011Y "hi” 
B 2012Y NULL 
B 2013Y “hello!” 
 4828 
Example 3:  DS_r := time_shift ( DS_3 , 1  )  results in: 4829 
 4830 
DS_r 
Id_1 Id_2 Me_1 
A 2011Y "hello world" 
145 
 
A 2012Y NULL 
A 2013Y "say hello" 
A 2014Y "he" 
B 2011Y "hi, hello! " 
B 2012Y "hi” 
B 2013Y NULL 
B 2014Y “hello!” 
 4831 
 4832 
Given the Data Set  DS_4, which contains both quarterly and annual time series relevant to the same 4833 
phenomenon “A”, where Id_2 is the reference time Identifier of  time_period type: 4834 
 4835 
DS_4 
Id_1 Id_2 Me_1 
A 2010Y "hello world" 
A 2011Y NULL 
A 2012Y "say hello" 
A 2013Y "he" 
A 2010Q1 "hi, hello! " 
A 2010Q2 "hi” 
A 2010Q3 NULL 
A 2010Q4 “hello!” 
 4836 
Example 4:  DS_r := time_shift ( DS_3 ,  -1  ) results in: 4837 
 4838 
DS_r 
Id_1 Id_2 Me_1 
A 2009Y "hello world" 
A 2010Y NULL 
A 2011Y "say hello" 
A 2012Y "he" 
A 2009Q4 "hi, hello! " 
A 2010Q1 "hi” 
A 2010Q2 NULL 
A 2010Q3 “hello!” 
 4839 
Time aggregation :  time_agg  4840 
The operator time_agg converts time, date and time_period values from a smaller to a larger duration. 4841 
 4842 
Syntax 4843 
time_agg ( periodIndTo { , periodIndFrom } { , op  } { , first | last }   )  4844 
 4845 
Input parameters 4846 
146 
 
op  the scalar value, the Component or the Data Set to be converted. If not specified, then 4847 
time_agg is used in combination within an aggregation operator  4848 
periodIndFrom the source period indicator 4849 
periodIndTo the target period indicator 4850 
 4851 
 4852 
Examples of valid syntaxes 4853 
sum ( DS group all time_agg ( Me, “A” ) ) 4854 
time_agg ( “A”, cast ( “2012Q1”, time_period , ”YYYY\Qq” ) ) 4855 
time_agg(“M”, cast (“2012-12-23”, date, “YYYY-MM-DD”) ) 4856 
time_agg(“M”, DS1) 4857 
ds_2 := ds1[calc Me1 := time_agg(“M”,Me1)] 4858 
 4859 
Semantics for scalar operations 4860 
The operator converts a time, date or time_period value from a smaller to a larger duration. 4861 
 4862 
Input parameters type 4863 
op ::  dataset { identifier < time > _ , identifier _* } 4864 
 |  component<time>  4865 
|  time   4866 
periodIndFrom ::  duration 4867 
periodIndTo ::  duration 4868 
 4869 
Result type 4870 
op ::  dataset { identifier < time > _ , identifier _* } 4871 
 |  component<time>  4872 
|  time   4873 
 4874 
Additional constraints 4875 
If op is a Data Set then it has exactly an Identifier of type time, date or time_period and may have other Identifiers. 4876 
It is only possible to convert smaller duration values to larger duration values (e.g. it is possible to convert 4877 
monthly data to annual data but the contrary is not allowed). 4878 
 4879 
Behaviour 4880 
The scalar version of this operator takes as input a time, date or time_period value, converts it  to periodIndTo 4881 
and returns a scalar of the corresponding type.  4882 
The Data Set version acts on a single Measure Data Set of type time, date  or time_period and returns a Data Set 4883 
having the same structure.  4884 
Finally, VTL also provides a component version, for use in combination with an aggregation operator, because 4885 
the change of frequency requires an aggregation. In this case, the operator converts the period_indicator of the 4886 
data points (e.g., convert monthly data to annual data).  4887 
On time type, the operator maps the input value into the comprising larger regular interval, whose duration is 4888 
the one specified by the periodIndTo parameter.  4889 
On date type, the operator maps the input value into the comprising larger period, whose duration is the one 4890 
specified by the periodIndTo parameter, which is conventionally represented either by the start or by the end 4891 
date, according to the first/last parameter. 4892 
On time_period type, the operator maps the input value into the comprising larger time period specified by the 4893 
periodIndTo parameter (the original period indicator is converted in the target one and the number of periods is 4894 
adjusted correspondingly).  4895 
The input duration periodIndFrom is optional. In case of time_period Data Points, the input duration can be 4896 
inferred from the internal representation of the value. In case of time or date types, it is inferred by the 4897 
implementation. Filters on input time series can be obtained with the filter clause. 4898 
 4899 
 4900 
Examples 4901 
Given the Data Set DS_1 4902 
 4903 
147 
 
DS_1 
Id_1 Id_2 Me_1 
2010Q1 A 20 
2010Q2 A 20 
2010Q3 A 20 
2010Q1 B 50 
2010Q2 B 50 
2010Q1 C 10 
2010Q2 C 10 
 4904 
Example 1: DS_r := sum ( DS_1 ) group all time_agg ( “A” , _ , Me_1 ) results in: 4905 
 4906 
DS_r 
Id_1 Id_2 Me_1 
2010 A 60 
2011 B 100 
2010 C 20 
 4907 
 4908 
Example 2: DS_r := time _agg ( “Q”, cast ( “2012M01”, time_period, ”YYYY\MMM” ) )  4909 
 4910 
Returns: “2012Q1”. 4911 
 4912 
Example 3: The following example maps a date to quarter level, 2012 (end of the period). 4913 
 4914 
time_agg( “Q”, cast(“20120213”, date, ”YYYYMMDD”), _ , false )  4915 
 4916 
and produces a date value corresponding to the string “20120331” 4917 
 4918 
Example 4: The following example maps a date to year level, 2012 (beginning of the period). 4919 
 4920 
time_agg(cast( ”A”, “2012M1”, date, ”YYYYMMDD”), _, true )  4921 
 4922 
and produces a date value corresponding to the string “20120101”. 4923 
 4924 
Actual time :     current_date  4925 
 4926 
Syntax 4927 
current_date ( )   4928 
 4929 
Input parameters 4930 
None 4931 
 4932 
Examples of valid syntax 4933 
current_date  4934 
 4935 
Semantics for scalar operations 4936 
The operator current_date returns the current time as a date type. 4937 
148 
 
 4938 
Input parameters type 4939 
This operator has no input parameters. 4940 
 4941 
Result type 4942 
result ::       date    4943 
 4944 
Additional constraints 4945 
None. 4946 
 4947 
Behaviour  4948 
The operator return the current date  4949 
 4950 
Examples 4951 
cast ( current_date, string, "YYYY.MM.DD" ) 4952 
  4953 
149 
 
VTL-ML  -  Set operators 4954 
Union:    union 4955 
 4956 
Syntax   4957 
union ( dsList ) 4958 
 4959 
 dsList ::= ds { , ds }* 4960 
 4961 
Input parameters 4962 
dsList    the list of Data Sets in the union 4963 
 4964 
Examples of valid syntaxes  4965 
union ( ds2, ds3 ) 4966 
 4967 
Semantics for scalar operations 4968 
This operator does not perform scalar operations. 4969 
 4970 
Input parameters type 4971 
ds  ::  dataset 4972 
 4973 
Result type 4974 
result ::   dataset    4975 
 4976 
Additional constraints 4977 
All the Data Sets in dsList have the same Identifier, Measure and Attribute Components. 4978 
 4979 
Behaviour 4980 
The union operator implements the union of functions (i.e., Data Sets). The resulting Data Set has the same 4981 
Identifier, Measure and Attribute Components of the operand Data Sets specified in the dsList, and contains the 4982 
Data Points belonging to any of the operand Data Sets.  4983 
The operand Data Sets can contain Data Points having the same values of the Identifiers. To avoid duplications of 4984 
Data Points in the resulting Data Set, those Data Points are filtered by chosing the Data Point belonging to the left 4985 
most operand Data Set. For instance, let's assume that in union ( ds1, ds2 ) the operand ds1 contains a Data 4986 
Point dp1 and the operand ds2 contains a Data Point dp2 such that dp1 has the same Identifiers values of dp2, 4987 
then the resulting Data Set contains dp1 only. 4988 
The operator has the typical behaviour of the “Behaviour of the Set operators” (see the section “Typical 4989 
behaviours of the ML Operators”).  4990 
The automatic Attribute propagation is not applied.   4991 
 4992 
Examples 4993 
 4994 
Given  the operand Data Sets DS_1 and DS_2: 4995 
 4996 
DS_1 
Id_1 Id_2 Id_3 Id_4 Me_1 
2012 B Total Total 5 
2012 G Total Total 2 
2012 F Total Total 3 
 4997 
 4998 
DS_2 
Id_1 Id_2 Id_3 Id_4 Me_1 
150 
 
2012 N Total Total 23 
2012 S Total Total 5 
 4999 
 5000 
Example 1:  DS_r := union(DS_1,DS_2)  results in: 5001 
 5002 
DS_r 
Id_1 Id_2 Id_3 Id_4 Me_1 
2012 B Total Total 5 
2012 G Total Total 2 
2012 F Total Total 3 
2012 N Total Total 23 
2012 S Total Total 5 
 5003 
Given  the operand Data Sets DS_1 and DS_2: 5004 
 5005 
DS_1 
Id_1 Id_2 Id_3 Id_4 Me_1 
2012 B Total Total 5 
2012 G Total Total 2 
2012 F Total Total 3 
 5006 
 5007 
DS_2 
Id_1 Id_2 Id_3 Id_4 Me_1 
2012 B Total Total 23 
2012 S Total Total 5 
 5008 
 5009 
Example 2: DS_r := union ( DS_1, DS_2 )  results in: 5010 
 5011 
DS_r 
Id_1 Id_2 Id_3 Id_4 Me_1 
2012 B Total Total 5 
2012 G Total Total 2 
2012 F Total Total 3 
2012 S Total Total 5 
Intersection :    intersect 5012 
Syntax   5013 
intersect ( dsList ) 5014 
 5015 
 dsList ::= ds { , ds }* 5016 
 5017 
Input parameters 5018 
dsList  the list of Data Sets in the intersection 5019 
151 
 
 5020 
Examples of valid syntaxes  5021 
intersect ( ds2, ds3 ) 5022 
 5023 
Semantics for scalar operations 5024 
This operator cannot be applied to scalar values. 5025 
  5026 
Input parameters type 5027 
ds  ::  dataset 5028 
 5029 
Return type 5030 
result ::       dataset    5031 
 5032 
Additional constraints 5033 
All the Data Sets in dsList have the same Identifier, Measure and Attribute Components. 5034 
 5035 
Behaviour 5036 
The intersect operator implements the intersection of functions (i.e., Data Sets). The resulting Data Set has the 5037 
same Identifier, Measure and Attribute Components of the operand Data Sets specified in the dsList, and 5038 
contains the Data Points belonging to all the operand Data Sets.  5039 
The operand Data Sets can contain Data Points having the same values of the Identifiers. To avoid duplications of 5040 
Data Points in the resulting Data Set, those Data Points are filtered by chosing the Data Point belonging to the left 5041 
most operand Data Set. For instance, let's assume that in intersect ( ds1, ds2 ) the operand ds1 contains a Data 5042 
Point dp1 and the operand ds2 contains a Data Point dp2 such that dp1 has the same Identifiers values of dp2, 5043 
then the resulting Data Set contains dp1 only. 5044 
The operator has the typical behaviour of the “Behaviour of the Set operators” (see the section “Typical 5045 
behaviours of the ML Operators”).   5046 
The automatic Attribute propagation is not applied.   5047 
 5048 
Examples 5049 
Given  the operand Data Sets DS_1 and DS_2: 5050 
 5051 
DS_1 
Id_1 Id_2 Id_3 Id_4 Me_1 
2012 B Total Total 1 
2012 G Total Total 2 
2012 F Total Total 3 
 5052 
 5053 
DS_2 
Id_1 Id_2 Id_3 Id_4 Me_1 
2011 B Total Total 10 
2012 G Total Total 2 
2011 M Total Total 40 
 5054 
Example 1:  DS_r := intersect(DS_1,DS_2)   results in: 5055 
 5056 
DS_1 
Id_1 Id_2 Id_3 Id_4 Me_1 
2012 G Total Total 2 
 5057 
152 
 
Set difference :     setdiff 5058 
 5059 
Syntax   5060 
setdiff ( ds1, ds2 ) 5061 
 5062 
Input parameters 5063 
ds1 the first Data Set in the difference (the minuend) 5064 
ds2  the second Data Set in the difference (the subtrahend) 5065 
 5066 
Examples of valid syntaxes  5067 
setdiff (ds2, ds3 ) 5068 
 5069 
Semantics for scalar operations 5070 
This operator cannot be applied to scalar values.  5071 
 5072 
Input parameters type 5073 
ds1, ds2 :: dataset 5074 
 5075 
Result type 5076 
result ::   dataset    5077 
 5078 
Additional constraints 5079 
The operand Data Sets have the same Identifier, Measure and Attribute Components. 5080 
 5081 
Behaviour 5082 
The operator implements the set difference of functions (i.e. Data Sets), interpreting the Data Points of the input 5083 
Data Sets as the elements belonging to the operand sets, the minuend and the subtrahend, respectively. The 5084 
operator returns one single Data Set, with the same Identifier, Measure and Attribute Components as the 5085 
operand Data Sets, containing the Data Points that appear in the first Data Set but not in the second. In other 5086 
words, for setdiff (ds1, ds2), the resulting Dataset contains all the data points Data Point dp1 of the operand ds1 5087 
such that there is no Data Point dp2 of ds2 having the same values for homonym Identifier Components. 5088 
The operator has the typical behaviour of the “Behaviour of the Set operators” (see the section “Typical 5089 
behaviours of the ML Operators”).   5090 
The automatic Attribute propagation is not applied.   5091 
 5092 
Examples 5093 
Given  the operand Data Sets DS_1 and DS_2: 5094 
 5095 
DS_1 
Id_1 Id_2 Id_3 Id_4 Me_1 
2012 B Total Total 10 
2012 G Total Total 20 
2012 F Total Total 30 
2012 M Total Total 40 
2012 I Total Total 50 
2012 S Total Total 60 
 5096 
 5097 
 5098 
DS_2 
Id_1 Id_2 Id_3 Id_4 Me_1 
2011 B Total Total 10 
2012 G Total Total 20 
153 
 
2012 F Total Total 30 
2012 M Total Total 40 
2012 I Total Total 50 
2012 S Total Total 60 
 5099 
Example 1: DS_r := setdiff ( DS_1, DS_2 ) results in: 5100 
 5101 
DS_r 
Id_1 Id_2 Id_3 Id_4 Me_1 
2012 B Total Total 10 
 5102 
Given the operand Data Sets DS_1 and DS_2 :  5103 
 5104 
DS_1 
Id_1 Id_2 Id_3 Me_1 
R M 2011 7 
R F 2011 10 
R T 2011 12 
 5105 
 5106 
DS_2 
Id_1 Id_2 Id_3 Me_1 
R M 2011 7 
R F 2011 10 
 5107 
Example 2:  DS_r := setdiff ( DS_1 , DS_2 )  results in: 5108 
 5109 
DS_r 
Id_1 Id_2 Id_3 Me_1 
R T 2011 12 
 5110 
 5111 
Simmetric difference :   symdiff 5112 
 5113 
Syntax   5114 
symdiff ( ds1, ds2 ) 5115 
 5116 
Input parameters 5117 
ds1 the first Data Set in the difference 5118 
ds2 the second Data Set in the difference 5119 
 5120 
Examples of valid syntaxes  5121 
symdiff (ds_2, ds_3) 5122 
 5123 
Semantics for scalar operations 5124 
This operator cannot be applied to scalar values.  5125 
 5126 
Input parameters type 5127 
154 
 
ds1, ds2  ::  dataset 5128 
 5129 
Result type 5130 
result ::       dataset    5131 
 5132 
Additional constraints 5133 
The operand Data Sets have the same Identifier, Measure and Attribute Components. 5134 
 5135 
Behaviour 5136 
The operator implements the symmetric set difference between functions (i.e. Data Sets), interpreting the Data 5137 
Points of the input Data Sets as the elements in the operand Sets. The operator returns one Data Set, with the 5138 
same Identifier, Measure and Attribute Components as the operand Data Sets, containing the Data Points that 5139 
appear in the first Data Set but not in the second and the Data Points that appear in the second Data Set but not 5140 
in the first one. 5141 
Data Points are compared to one another by Identifier Components. For symdiff (ds1, ds2), the resulting Data 5142 
Set contains all the Data Points dp1 contained in ds1 for which there is no Data Point dp2 in ds2 with the same 5143 
values for homonym Identifier components and all the Data Points dp2 contained in ds2 for which there is no 5144 
Data Point dp1 in ds1 with the same values for homonym Identifier Components. 5145 
The operator has the typical behaviour of the “Behaviour of the Set operators” (see the section “Typical 5146 
behaviours of the ML Operators”).   5147 
The automatic Attribute propagation is not applied.  5148 
  5149 
Examples 5150 
Given the operand Data Sets DS_1 and DS_2 : 5151 
 5152 
DS_1 
Id_1 Id_2 Id_3 Id_4 Me_1 
2012 B Total Total 1 
2012 G Total Total 2 
2012 F Total Total 3 
2012 M Total Total 4 
2012 I Total Total 5 
2012 S Total Total 6 
 5153 
 5154 
DS_2 
Id_1 Id_2 Id_3 Id_4 Me_1 
2011 B Total Total 1 
2012 G Total Total 2 
2012 F Total Total 3 
2012 M Total Total 4 
2012 I Total Total 5 
2012 S Total Total 6 
 5155 
Example 1:  DS_r := symdiff ( DS_1, DS_2 )  results in: 5156 
 5157 
DS_r 
Id_1 Id_2 Id_3 Id_4 Me_1 
2012 B Total Total 1 
2011 B Total Total 1 
 5158 
155 
 
VTL-ML  -  Hierarchical aggregation 5159 
Hierarchical roll-up :  hierarchy 5160 
Syntax 5161 
hierarchy ( op , hr { condition condComp { , condComp }* } { rule ruleComp } { mode } { input } { output } ) 5162 
mode ::=  non_null | non_zero | partial_null | partial_zero | always_null | always_zero 5163 
input ::=  dataset | rule | rule_priority  5164 
output ::=  computed | all 5165 
 5166 
Input parameters 5167 
op    the operand Data Set. 5168 
hr    the hierarchical Ruleset to be applied. 5169 
condComp  condComp is a Component of op to be associated (in positional order) to the 5170 
conditioning Value Domains or Variables defined in hr (if any). 5171 
ruleComp ruleComp is the Identifier of op to be associated to the rule Value Domain or Variable 5172 
defined in hr. 5173 
mode this parameter specifies how to treat the possible missing Data Points corresponding to 5174 
the Code Items in the right side of a rule and which Data Points are produced in output. 5175 
The meaning of the possible values of the parameter is explained below. 5176 
input this parameter specifies the source of the values used as input of the hierarchical rules. 5177 
The meaning of the possible values of the parameter is explained below. 5178 
output this parameter specifies the content of the resulting Data Set. The meaning of the 5179 
possible values of the parameter is explained below. 5180 
 5181 
Examples of valid syntaxes  5182 
hierarchy ( DS1, HR1  rule Id_1 non_null all )  5183 
hierarchy ( DS2, HR2  condition Comp_1, Comp_2 rule Id_3 non_zero rule computed )  5184 
 5185 
Semantics for scalar operations 5186 
This operator cannot be applied to scalar values.  5187 
 5188 
Input parameters type 5189 
op ::  dataset { measure<number> _ }  5190 
hr ::  name <  hierarchical >  5191 
condComp ::  name < component > 5192 
ruleComp ::  name < dentifier > 5193 
 5194 
Result type 5195 
result ::   dataset {measure<number> _ }     5196 
 5197 
Additional constraints 5198 
If hr is defined on Value Domains then it is mandatory to specify the condition (if any) and the rule parameters. 5199 
Moreover, the Components specified as condComp and ruleComp must belong to the operand op and must take 5200 
values on the Value Domains corresponding, in positional order, to the ones specified in the condition and rule 5201 
parameter of hr. 5202 
If hr is defined on Variables, the specification of condComp and ruleComp is not needed, but they can be 5203 
specified all the same if it is desired to show explicitly in the invocation which are the involved Components: in 5204 
this case, the condComp and ruleComp  must be the same and in the same order as the Variables specified in in 5205 
the condition and rule signatures of hr.  5206 
 5207 
Behaviour 5208 
The hierarchy operator applies the rules of hr to op as specified in the parameters. The operator returns a Data 5209 
Set with the same Identifiers and the same Measure as op. The Attribute propagation rule is applied on the 5210 
groups of Data Points which contribute to the same Data Points of the result.  5211 
The behaviours relevanto to the different options of the input parameters are the following. 5212 
156 
 
First, the parameter input is considered to determine the source of the Data Points used as input of the 5213 
Hierarchy. The possible options of the parameter input and the corresponding behaviours are the following: 5214 
dataset  For each Rule of the Ruleset and for each item on the right hand side of the Rule, the operator 5215 
takes the input Data Points exclusively from the operand op. 5216 
rule For each Rule of the Ruleset and for each item on the right-hand side of the Rule: 5217 
 if the item is not defined as the result (left-hand side) of another Rule, the current Rule 5218 
takes the input Data Points from the operand op  5219 
 if the item is defined as the result of another Rule, the current Rule takes the input Data 5220 
Points from the computed output of such other Rule; 5221 
rule_priority  For each Rule of the Ruleset and for each item on the right-hand side of the Rule:  5222 
 if the item is not defined as the result (left-hand side) of another rule, the current Rule 5223 
takes the input Data Points from the operand op.  5224 
 if the item is defined as the result of another Rule, then: 5225 
o if an expected input Data Point exists in the computed output of such other Rule 5226 
and its Measure is not NULL, then the current Rule takes such Data Point;  5227 
o if an expected input Data Point does not exist in the computed output of such 5228 
other Rule or its measure is NULL, then the current Rule takes the Data Point 5229 
from op (if any) having the same values of the Identifiers;  5230 
if the parameter input is not specified then it is assumed to be rule. 5231 
Then the parameter mode is considered, to determine the behaviour for missing Data Points and for the Data 5232 
Points to be produced in the output. The possible options of the parameter mode and the corresponding 5233 
behaviours are the following: 5234 
non_null the result Data Point is produced when its computed Measure value is not NULL (i.e., when no 5235 
Data Point corresponding to the Code Items of the right side of the rule is missing or has NULL 5236 
Measure value); in the calculation, the possible missing Data Points corresponding to the Code 5237 
Items of the right side of the rule are considered existing and having a Measure value equal to 5238 
NULL;  5239 
non_zero the result Data Point is produced when its computed Measure value is not equal to 0 (zero); 5240 
the possible missing Data Points corresponding to the Code Items of the right side of the rule 5241 
are considered existing and having a Measure value equal to 0;  5242 
partial_null the result Data Point is produced if at least one Data Point corresponding to the Code Items of 5243 
the right side of the rule is found (whichever is its Measure value); the possible missing Data 5244 
Points corresponding to the Code Items of the right side of the rule are considered existing and 5245 
having a NULL Measure value;  5246 
partial_zero the result Data Point is produced if at least one Data Point corresponding to the Code Items of 5247 
the right side of the rule is found (whichever is its Measure value); the possible missing Data 5248 
Points corresponding to the Code Items of the right side of the rule are considered existing and 5249 
having a Measure value equal to 0 (zero); 5250 
always_null the result Data Point is produced in any case; the possible missing Data Points corresponding 5251 
to the Code Items of the right side of the rule are considered existing and having have a 5252 
Measure value equal to NULL;  5253 
always_zero the result Data Point is produced in any case; the possible missing Data Points corresponding 5254 
to the Code Items of the right side of the rule are considered existing and having a Measure 5255 
value equal to 0 (zero); 5256 
If the parameter mode is not specified, then it is assumed to be non_null 5257 
 5258 
The following table summarizes the behaviour of the options of the parameter “mode” 5259 
 5260 
OPTION of the 
MODE 
PARAMETER: 
Missing Data 
Points are 
considered: 
Null Data 
Points are 
considered: 
Condition for 
evaluating the rule 
Returned Data 
Points 
Non_null NULL NULL If all the involved Data 
Points are not NULL 
Only not NULL 
Data Points (Zeros 
are returned too) 
Non_zero Zero NULL 
If at least one of the 
involved Data Points is 
<> zero 
Only not zero Data 
Points  (NULLS are 
returned too) 
157 
 
Partial_null NULL NULL 
If at least one of the 
involved  Data Points 
is not NULL 
Data Points of any 
value (NULL, not 
NULL and zero too) 
Partial_zero Zero NULL 
If at least one of the 
involved  Data Points 
is not NULL 
Data Points of any 
value (NULL, not 
NULL and zero too) 
Always_null NULL NULL Always 
Data Points of any 
value (NULL, not 
NULL and zero too) 
Always_zero Zero NULL Always 
Data Points of any 
value (NULL, not 
NULL and zero too) 
 5261 
Finally the parameter output is considered, to determine the content of the resulting Data Set. The possible 5262 
options of the parameter output and the corresponding behaviours are the following: 5263 
computed the resulting Data Set contains only the set of Data Points computed according to the Ruleset 5264 
all the resulting Data Set contains the union between the set of Data Points “R” computed 5265 
according to the Ruleset and the set of Data Points of op that have different combinations of 5266 
values for the Identifiers. In other words, the result is the outcome of the following (virtual) 5267 
expression:  union ( setdiff (op , R) , R ) 5268 
If the parameter output is not specified then it is assumed to be computed. 5269 
 5270 
Examples 5271 
Given the following hierarchical ruleset: 5272 
 5273 
define hierarchical ruleset  HR_1 ( valuedomain rule  VD_1 )  is 5274 
   A = J + K + L 5275 
;  B = M + N + O 5276 
;  C = P + Q 5277 
;  D = R + S 5278 
;  E = T + U + V 5279 
;  F = Y + W + Z  5280 
;  G = B + C 5281 
;  H = D + E 5282 
;  I  = D + G 5283 
end hierarchical ruleset 5284 
 5285 
And given  the operand Data Set DS_1  (where At_1 is viral and the propagation rule says that the alphabetic 5286 
order prevails the NULL prevails on the alphabetic characters and the Attribute value for missing Data Points 5287 
is assumed as NULL): 5288 
 5289 
DS_1 
Id_1 Id_2 Me_1 At_1 
2010 M 2 Dx 
2010 N 5 Pz 
2010 O 4 Pz 
2010 P 7 Pz 
2010 Q -7 Pz 
2010 S 3 Ay 
2010 T 9 Bq 
2010 U NULL Nj 
158 
 
2010 V 6 Ko 
 5290 
 5291 
Example 1: DS_r := hierarchy ( DS_1, HR_1 rule Id_2 non_null )  results in: 5292 
 5293 
DS_r 
Id_1 Id_2 Me_1 At_1 
2010 B 11 Dx 
2010 C 0 Pz 
2010 G 19 Dx 
 5294 
 5295 
Example 2:   DS_r := hierarchy ( DS_1, HR_1 rule Id_2 non_zero )  results in: 5296 
 5297 
DS_r 
Id_1 Id_2 Me_1 At_1 
2010 B 11 Dx 
2010 D 3 NULL 
2010 E NULL Bq 
2010 G 11 Dx 
2010 H NULL NULL 
2010 I 14 NULL 
 5298 
 5299 
Example 2:   DS_r := hierarchy ( DS_1, HR_1 rule Id_2 partial_null )  results in: 5300 
 5301 
DS_r 
Id_1 Id_2 Me_1 At_1 
2010 B 11 Dx 
2010 C 0 Pz 
2010 D NULL NULL 
2010 E NULL Bq 
2010 G 11 Dx 
2010 H NULL NULL 
2010 I NULL NULL 
 5302 
 5303 
159 
 
VTL-ML  -  Aggregate and Analytic operators 5304 
 5305 
The following table lists the operators that can be invoked in the Aggregate or in the Analytic invocations 5306 
described below and their main characteristics. 5307 
 5308 
Operator Description Allowed 
invocations 
Type of the resulting 
Measure 
Type of the operand 
Measures 
count  number of Data Points Aggregate  
Analytic 
integer any 
min  minimum value of a set of values Aggregate  
Analytic 
any any 
max  maximum value of a set of values Aggregate  
Analytic 
any any 
median  median value of a set of numbers Aggregate 
Analytic 
number number 
sum sum of a set of numbers Aggregate  
Analytic 
number number 
avg  average value of a set of numbers Aggregate  
Analytic 
number number  
stddev_pop population standard deviation of a 
set of numbers 
Aggregate  
Analytic 
number number 
stddev_samp sample standard deviation of a set 
of numbers 
Aggregate 
Analytic 
number number 
var_pop population variance of a set of 
numbers 
Aggregate  
Analytic 
number number 
var_samp sample variance of a set of 
numbers 
Aggregate  
Analytic 
number number 
first_value first value in an ordered set of 
values 
Analytic any any 
last_value last value in an ordered set of 
values 
Analytic any any 
lag in an ordered set of Data Points, it 
returns the value(s) taken from a 
Data Point at a given physical 
offset prior to the current Data 
Point 
Analytic any any  
lead in an ordered set of Data Points, it 
returns the value(s) taken from a 
Data Point at a given physical 
offset beyond the current Data 
Point 
Analytic any any  
rank rank (order number) of a Data 
Point in an ordered set of Data 
Points  
Analytic integer any 
160 
 
ratio_to_report ratio of a value to the sum of a set 
of values 
Analytic number number 
 5309 
Aggregate invocation  5310 
Syntax 5311 
 5312 
in a Data Set expression: 5313 
aggregateOperator ( firstOperand  { , additionalOperand }*   { groupingClause }  )   5314 
 5315 
in a Component  expression within an aggr clause) 5316 
aggregateOperator ( firstOperand { , additionalOperand }* )  { groupingClause }  5317 
 5318 
 5319 
aggregateOperator ::=   avg | count | max | median | min | stddev_pop 5320 
  | stddev_samp | sum | var_pop | var_samp  5321 
groupingClause ::=  { group by groupingId {, groupingId}*  5322 
 |   group except groupingId {, groupingId}*  5323 
 |   group all conversionExpr }1    5324 
 { having havingCondition } 5325 
    5326 
 5327 
Input Parameters 5328 
aggregateOperator the keyword of the aggregate operator to  invoke (e.g.,  avg, count, max …) 5329 
firstOperand the first operand of the invoked aggregate operator (a Data Set for an invocation at 5330 
Data Set level or a Component of the input Data Set for an invocation at Component 5331 
level within a aggr operator or a aggr clause in a join operation) 5332 
additionalOperand  an additional operand (if any) of the invoked operator. The various operators can have 5333 
a different number of parameters. The number of parameters, their types and if they 5334 
are mandatory or optional depend on the invoked operator 5335 
groupingClause the following alternative grouping options: 5336 
group by the Data Points are grouped by the values of the specified Identifiers 5337 
(groupingId). The Identifiers not specified are dropped in the result. 5338 
group except the Data Points are grouped by the values of the Identifiers not 5339 
specified as groupingId. The Identifiers specified as groupingId are 5340 
dropped in the result. 5341 
group all converts the values of an Identifier Component using conversionExpr 5342 
and keeps all the resulting Identifiers. 5343 
groupingId Identifier Component to be kept (in the group by clause) or dropped (in the group 5344 
except clause). 5345 
conversionExpr specifies a conversion operator (e.g., time_agg) to convert data from finer to coarser 5346 
granularity. The conversion operator is applied on an Identifier of the operand Data 5347 
Set op. 5348 
havingCondition a condition (boolean expression) at component level, having only Components of the 5349 
input Data Sets as operands (and possibly constants), to be fulfilled by the groups of 5350 
Data Points:  only groups for which havingCondition evaluates to TRUE appear in the 5351 
result. The havingCondition refers to the groups specified through the 5352 
groupingClause, therefore it must invoke aggregate operators (e.g.  avg, count, max 5353 
…,  see also the corresponding sections). A correct example of havingCondition is: 5354 
max(obs_value) < 1000  5355 
while the condition obs_value < 1000 is not a right havingCondition, because it refers 5356 
to the values of single Data Points and not to the groups. The count operator is used in 5357 
a havingCondition without parameters, e.g.:  5358 
sum ( ds group by id1 having count ( ) >= 10 ) 5359 
 5360 
Examples of valid syntaxes   5361 
avg ( DS_1 ) 5362 
avg ( DS_1 group by Id_1, Id_2  ) 5363 
161 
 
avg ( DS_1 group except  Id_1, Id_2  ) 5364 
avg ( DS_1 group all time_agg ( "Q" ) ) 5365 
 5366 
Semantics for scalar operations 5367 
The aggregate operators cannot be applied to scalar values.  5368 
 5369 
Input parameters type  5370 
firstOperand ::    dataset  5371 
| component 5372 
additionalOperand :: see the type of the additional parameter (if any) of the invoked  5373 
aggregateOperator. The aggregate operators and their parameters are 5374 
described in the following sections. 5375 
groupingId ::   name < identifier > 5376 
conversionExpr ::   identifier    5377 
havingCondition ::  component<boolean> 5378 
 5379 
Result type: 5380 
result ::    dataset 5381 
| component 5382 
 5383 
Additional constraints 5384 
The Aggregate invocation cannot be nested in other Aggregate or Analytic invocations.  5385 
The aggregate operations at component level can be invoked within the aggr clause, both as part of a join 5386 
operator and the aggr operator (see the parameter aggrExpr of those operators).  5387 
The basic scalar types of firstOperand and additionalOperand (if any) must be compliant with the specific basic 5388 
scalar types required by the invoked operator (the required basic scalar types are described in the table at the 5389 
beginning of this chapter and in the sections of the various operators below). 5390 
The conversionExpr parameter applies just one conversion operator to just one Identifier belonging to the input 5391 
Data Set. The basic scalar type of the Identifier must be compatible with the basic scalar type of the conversion 5392 
operator.  5393 
If the grouping clause is omitted, then all the input Data Points are aggregated in a single group and the clause 5394 
returns a Data Set that contains a single Data Point and has no Identifiers. 5395 
 5396 
Behaviour 5397 
The aggregateOperator is applied as usual to all the measures of the firstOperand Data Set (if invoked at Data 5398 
Set level) or to the firstOperand Component of the input Data Set (if invoked at Component level).  In both cases, 5399 
the operator calculates the required aggregated values for groups of Data Points of the input Data Set. The 5400 
groups of Data Points to be aggregated are specified through the groupingClause, which allows the following 5401 
alternative options. 5402 
 5403 
group by the Data Points are grouped by the values of the specified Identifiers. The Identifiers not 5404 
specified are dropped in the result. 5405 
group except the Data Points are grouped by the values of the Identifiers not specified in the clause. The 5406 
specified Identifiers are dropped in the result. 5407 
group all converts an Identifier Component using conversionExpr and keeps all the Identifiers. 5408 
 5409 
The having clause is used to filter groups in the result by means of an aggregate condition evaluated on the 5410 
single groups (for example the minimum number of rows in the group). 5411 
If no grouping clause is specified, then all the input Data Points are aggregated in a single group and the operator 5412 
returns a Data Set that contains a single Data Point and has no Identifiers. 5413 
For the invocation at Data Set level, the resulting Data Set has the same Measures as the operand. For the 5414 
invocation at Component level, the resulting Data Set has the Measures explicitly calculated (all the other 5415 
Measures are dropped because no aggregation behaviour is specified for them). 5416 
For invocation at Data Set level, the Attribute propagation rule is applied.  For invocation at Component level,  5417 
the Attributes calculated within the aggr clause are maintained in the result; for all the other Attributes that are 5418 
defined as viral, the Attribute propagation rule is applied (for the semantics, see the Attribute Propagation Rule 5419 
section in the User Manual). 5420 
As mentioned, the Aggregate invocation at component level can be done within the aggr clause, both as part of a 5421 
Join operator and the aggr operator (see the parameter aggrExpr of those operators), therefore, for a better 5422 
comprehension fo the behaviour at Component level, see also those operators.  5423 
162 
 
 5424 
 5425 
Examples 5426 
 5427 
Given the Data Set DS_1 5428 
 5429 
DS_1 
Id_1 Id_2 Id_3 Me_1 At_1 
2010 E XX 20  
2010 B XX 1 H 
2010 R XX 1 A 
2010 F YY 23  
2011 E XX 20 P 
2011 B ZZ 1 N 
2011 R YY -1 P 
2011 F XX 20 Z 
2012 L ZZ 40 P 
2012 E YY 30 P 
 5430 
Example1:  DS_r := avg ( DS_1  group by  Id_1 )  provided that At_1 is non viral,  results in: 5431 
 5432 
DS_r 
Id_1 Me_1 
2010 11.25 
2011 10 
2012 35 
 5433 
Note: the example above can be rewritten equivalently in the following forms: 5434 
 5435 
DS_r := avg ( DS_1  group except   Id_2,  Id_3 ) 5436 
DS_r := avg ( DS_1#Me_1  group by  Id_1 ) 5437 
 5438 
Example2:  DS_r := sum ( DS_1  group by  Id_1, Id_3  )  provided that At_1 is non viral,  results in: 5439 
 5440 
DS_r 
Id_1 Id_3 Me_1 
2010 XX 22 
2010 YY 23 
2011 XX 40 
2011 ZZ 1 
2011 YY -1 
2012 ZZ 40 
2012 YY 30 
 5441 
Example3:  DS_r := avg ( DS_1 )  provided that At_1 is non viral  results in: 5442 
 5443 
163 
 
DS_r 
Me_1 
15.5 
 5444 
Example4:  DS_r := DS_1 [ aggr Me_2 := max ( Me_1 ) , Me_3 := min ( Me_1 ) group by Id_1 ]  5445 
  5446 
provided that At_1 is viral and the first letter in alphabetic order prevails and NULL prevails on 5447 
all the other characters, results in: 5448 
 5449 
DS_r 
Id_1 Me_2 Me_3 At_1 
2010 23 1  
2011 20 -1 N 
2012 40 30 P 
Analytic invocation 5450 
Syntax 5451 
analyticOperator ( firstOperand { , additionalOperand }*  over ( analyticClause ) ) 5452 
 5453 
analyticOperator  ::=  avg | count | max | median | min | stddev_pop 5454 
  | stddev_samp | sum | var_pop | var_samp  5455 
  | first_value | lag | last_value | lead | rank | ratio_to_report 5456 
analyticClause  ::= { partitionClause } { orderClause } { windowClause } 5457 
partitionClause  ::=  partition by identifier { ,  identifier }* 5458 
orderClause        ::=  order by component { asc | desc } { , component { asc | desc } }* 5459 
windowClause  ::= { data points | range }1  between limitClause and limitClause 5460 
limitClause           ::= { num preceding | num following | current data point | unbounded preceding |   5461 
unbounded following }1 5462 
Parameters 5463 
analyticOperator the keyword of the analytic operator to invoke (e.g.,  avg, count, max …) 5464 
firstOperand the first operand of the invoked analytic operator (a Data Set for an invocation at Data 5465 
Set level or a Component of the input Data Set for an invocation at Component level 5466 
within a calc operator or a calc clause in a join operation) 5467 
additionalOperand  an additional operand (if any) of the invoked operator. The various operators can have 5468 
a different number of parameters. The number of parameters, their types and if they 5469 
are mandatory or optional depend on the invoked operator 5470 
analyticClause clause that specifies the analytic behaviour 5471 
partitionClause clause that specifies how to partition Data Points in groups to be analysed separately. 5472 
The input Data Set is partitioned according to the values of one or more Identifier 5473 
Components. If the clause is omitted, then the Data Set is partitioned by the Identifier 5474 
Components that are not specified in the orderClause. 5475 
orderClause clause that specifies how to order the Data Points. The input Data Set is ordered 5476 
according to the values of one or more Components, in ascending order if asc is 5477 
specified, in descending order if desc is specified, by default in ascending order if the 5478 
asc and desc keywords are omitted. 5479 
windowClause clause that specifies how to apply a sliding window on the ordered Data Points. The 5480 
keyword data points means that the sliding window includes a certain number of 5481 
Data Points before and after the current Data Point in the order given by the 5482 
orderClause. The keyword range means that the sliding windows includes all the Data 5483 
Points whose values are in a certain range in respect to the value, for the current Data 5484 
Point, of the Measure which the analytic is applied to.  5485 
164 
 
limitClause clause that can specify either the lower or the upper boundaries of the sliding window. 5486 
Each boundary is specified in relationship either to the whole partition or to the 5487 
current data point under analysis by using the following keywords: 5488 
 unbounded preceding means that the sliding window starts at the first Data Point 5489 
of the partition (it make sense only as the first limit of the window) 5490 
 unbounded following indicates that the sliding window ends at the last Data Point 5491 
of the partition (it makes sense only as the second limit of the window) 5492 
 current data point specifies that the window starts or ends at the current Data 5493 
Point.  5494 
 num preceding specifies either the number of data points to consider preceding 5495 
the current data point in the order given by the orderClause (when data points is 5496 
specified in the window clause), or the maximum difference to consider, as for the 5497 
Measure which the analytic is applied to, between the value of the current Data 5498 
Point and the generic other Data Point  (when range is specified in the windows 5499 
clause).  5500 
 num following specifies either the number of data points to consider following the 5501 
current data point in the order given by the orderClause (when data points is 5502 
specified in the window clause), or the maximum difference to consider, as for the 5503 
Measure which the analytic is applied to, between the values of the generic other 5504 
Data Point and the current Data Point (when range is specified in the windows 5505 
clause).  5506 
If the whole windowClause is omitted then the default is data points between 5507 
unbounded preceding and current data point. 5508 
identifier an Identifier Component of the input Data Set 5509 
component a Component of the input Data Set 5510 
num a scalar number    5511 
 5512 
Examples of valid syntaxes 5513 
sum ( DS_1 over ( partition by  Id_1  order by  Id_2  ) ) 5514 
sum ( DS_1 over ( order by  Id_2  ) ) 5515 
avg ( DS_1 over ( order by  Id_1  data points between 1 preceding and 1 following ) ) 5516 
DS_1 [ calc M1 := sum ( Me_1 over ( order by  Id_1  ) ) ] 5517 
 5518 
Semantics for scalar operations 5519 
The analytic operators cannot be applied to scalar values.  5520 
 5521 
Input parameters type 5522 
firstOperand ::                dataset 5523 
 |  component 5524 
additionalOperand :: see the type of the additional parameter (if any) of the invoked  operator. The operators 5525 
and their parameters are described in the following sections. 5526 
identifier ::   name < identifier > 5527 
component ::   name < component > 5528 
num ::    integer 5529 
 5530 
Result type 5531 
result ::    dataset 5532 
 |  component 5533 
 5534 
Additional constraints 5535 
The analytic invocation cannot be nested in other Aggregate or Analytic invocations.  5536 
The analytic operations at component level can be invoked within the calc clause, both as part of a Join operator 5537 
and the calc operator (see the parameter calcExpr of those operators).  5538 
The basic scalar types of firstOperand and additionalOperand (if any) must be compliant with the specific basic 5539 
scalar types required by the invoked operator (the required basic scalar types are described in the table at the 5540 
beginning of this chapter and in the sections of the various operators below). 5541 
 5542 
165 
 
Behaviour 5543 
The analytic Operator is applied as usual to all the Measures of the input Data Set (if invoked at Data Set level) or 5544 
to the specified Component of the input Data Set (if invoked at Component level).  In both cases, the operator 5545 
calculates the desired output values for each Data Point of the input Data Set. 5546 
The behaviour of the analytic operations can be procedurally described as follows: 5547 
 The Data Points of the input Data Set are first partitioned (according to partitionBy) and then ordered 5548 
(according to orderBy).  5549 
 The operation is performed for each Data Point (named “current Data Point”) of the input Data Set. For each 5550 
input Data Point,  one output Data Point is returned, having the same values of the Identifiers. The analytic 5551 
operator is applied to a “window” which includes a set of Data Points of the input Data Set and returns the 5552 
values of the Measure(s) of the output Data Point. 5553 
 If windowClause is not specified, then the set of Data Points which contribute to the analytic operation is 5554 
the whole partition which the current Data Point belongs to 5555 
 If windowClause is specified, then the set of Data Points is the one specified by windowClause (see 5556 
windowsClause and LimitClause explained above). 5557 
For the invocation at Data Set level, the resulting Data Set has the same Measures as the input Data Set 5558 
firstOperand. For the invocation at Component level, the resulting Data Set has the Measures of the input Data 5559 
Set plus the Measures explicitly calculated through the calc clause. 5560 
For the invocation at Data Set level, the Attribute propagation rule is applied.  For invocation at Component level,  5561 
the Attributes calculated within the calc clause are maintained in the result; for all the other Attributes that are 5562 
defined as viral, the Attribute propagation rule is applied (for the semantics, see the Attribute Propagation Rule 5563 
section in the User Manual). 5564 
As mentioned, the Analytic invocation at component level can be done within the calc clause, both as part of a 5565 
Join operator and the calc operator (see the parameter aggrCalc of those operators), therefore, for a better 5566 
comprehension fo the behaviour at Component level, see also those operators. 5567 
 5568 
Examples 5569 
 5570 
Given the Data Set DS_1: 5571 
 5572 
DS_r 
Id_1 Id_2 Id_3 Me_1 
2010 E XX 5 
2010 B XX -3 
2010 R XX 9 
2010 E YY 13 
2011 E XX 11 
2011 B ZZ 7 
2011 E YY -1 
2011 F XX 0 
2012 L ZZ -2 
2012 E YY 3 
 5573 
Example1:  5574 
  5575 
DS_r := sum ( DS_1 over ( order by  Id_1, Id_2, Id_3  data points between 1 preceding and 1 following ) ) 5576 
   results in: 5577 
 5578 
DS_r 
Id_1 Id_2 Id_3 Me_1 
166 
 
2010 B XX 2 
2010 E XX 15 
2010 E YY 27 
2010 R XX 29 
2011 B ZZ 27 
2011 E XX 17 
2011 E YY 10 
2011 F XX 2 
2012 E YY 1 
2012 L ZZ 1 
Counting the number of data points:  count 5579 
Aggregate syntax 5580 
count  ( dataset { groupingClause } )  (in a Data Set expression) 5581 
count  ( component  ) {  groupingClause }  (in a Component expression within an aggr clause)  5582 
count  ( )      (in an having clause) 5583 
 5584 
Analytic syntax 5585 
count  ( dataset over ( analyticClause ) )  (in a Data Set expression) 5586 
count  ( component over ( analyticClause ) ) (in a Component expression within a calc clause) 5587 
 5588 
Input parameters 5589 
dataset  the operand Data Set 5590 
component  the operand Component 5591 
groupingClause see Aggregate invocation  5592 
analyticClause see Analytic invocation 5593 
 5594 
Examples of valid syntaxes 5595 
See Aggregate and Analytic invocations above, at the beginning of the section. 5596 
 5597 
Semantics for scalar operations 5598 
This operator cannot be applied to scalar values.  5599 
 5600 
Input parameters type 5601 
dataset ::             dataset 5602 
component ::  component 5603 
 5604 
Result type 5605 
result ::     dataset  { measure<integer>  int_var  }   5606 
   |  component<integer> 5607 
 5608 
Additional constraints 5609 
None. 5610 
 5611 
Behaviour 5612 
The operator returns the number of the input Data Points. 5613 
For other details, see Aggregate and Analytic invocations. 5614 
 5615 
Examples 5616 
Given the Data Set DS_1: 5617 
167 
 
 5618 
DS_1 
Id_1 Id_2 Id_3 Me_1 
2011 A XX iii 
2011 A YY jjj 
2011 B YY iii 
2012 A XX kkk 
2012 B YY iii 
 5619 
 5620 
Example 1: DS_r := count ( DS_1 group by  Id_1  )   results in: 5621 
 5622 
DS_r 
Id_1 Int_var 
2011 3 
2012 2 
 5623 
Example 1: use of count in a having clause: 5624 
 5625 
DS_r := sum ( DS_1 group by  Id_1  having count() > 2 )  results in: 5626 
 5627 
DS_r 
Id_1 Int_var 
2011 3 
 5628 
Minimum value :  min 5629 
Aggregate syntax 5630 
min  ( dataset { groupingClause } )   (in a Data Set expression) 5631 
min  ( component ) { groupingClause }    (in a Component expression within an aggr clause)  5632 
 5633 
Analytic syntax 5634 
min  ( dataset over ( analyticClause ) )  (in a Data Set expression) 5635 
min  ( component over ( analyticClause ) )  (in a Component expression within a calc clause) 5636 
 5637 
Input parameters 5638 
dataset  the operand Data Set 5639 
component  the operand Component 5640 
groupingClause see Aggregate invocation  5641 
analyticClause see Analytic invocation 5642 
 5643 
Examples of valid syntaxes 5644 
See Aggregate and Analytic invocations above, at the beginning of the section. 5645 
 5646 
Semantics for scalar operations 5647 
This operator cannot be applied to scalar values.  5648 
 5649 
168 
 
Input parameters type 5650 
dataset ::              dataset 5651 
component ::       component 5652 
 5653 
Result type 5654 
result ::   dataset   5655 
 |  component 5656 
 5657 
Additional constraints 5658 
None. 5659 
 5660 
Behaviour 5661 
The operator returns the minimum value of the input values. 5662 
For other details, see Aggregate and Analytic invocations. 5663 
 5664 
Examples 5665 
Given the Data Set DS_1: 5666 
 5667 
DS_1 
Id_1 Id_2 Id_3 Me_1 
2011 A XX 3 
2011 A YY 5 
2011 B YY 7 
2012 A XX 2 
2012 B YY 4 
 5668 
Example 1: DS_r := min ( DS_1 group by  Id_1  )  results in: 5669 
 5670 
DS_r 
Id_1 Me_1 
2011 3 
2012 2 
Maximum value :  max 5671 
Aggregate syntax 5672 
max  ( dataset { groupingClause } )   (in a Data Set expression) 5673 
max  ( component ) { groupingClause }    (in a Component expression within an aggr clause)  5674 
 5675 
Analytic syntax 5676 
max  ( dataset over ( analyticClause ) )  (in a Data Set expression) 5677 
max  ( component over ( analyticClause ) )  (in a Component expression within a calc clause) 5678 
 5679 
Input parameters 5680 
dataset  the operand Data Set 5681 
component  the operand Component 5682 
groupingClause see Aggregate invocation  5683 
analyticClause see Analytic invocation 5684 
 5685 
169 
 
Examples of valid syntaxes 5686 
See Aggregate and Analytic invocations above, at the beginning of the section. 5687 
 5688 
Semantics for scalar operations 5689 
This operator cannot be applied to scalar values.  5690 
 5691 
Input parameters type 5692 
dataset ::              dataset 5693 
component ::          component 5694 
 5695 
Result type 5696 
result ::      dataset   5697 
  |  component 5698 
 5699 
Additional constraints 5700 
None. 5701 
 5702 
Behaviour 5703 
The operator returns the maximum of the input values. 5704 
For other details, see Aggregate and Analytic invocations. 5705 
 5706 
Examples 5707 
Given the Data Set DS_1: 5708 
 5709 
DS_1 
Id_1 Id_2 Id_3 Me_1 
2011 A XX 3 
2011 A YY 5 
2011 B YY 7 
2012 A XX 2 
2012 B YY 4 
 5710 
Example 1: DS_r := max ( DS_1 group by  Id_1  )  results in: 5711 
 5712 
DS_r 
Id_1 Me_1 
2011 7 
2012 4 
Median value :  median 5713 
Aggregate syntax 5714 
median  ( dataset { groupingClause } )  (in a Data Set expression) 5715 
median  ( component ) { groupingClause }    (in a Component expression within an aggr clause)  5716 
 5717 
Analytic syntax 5718 
median  ( dataset over ( analyticClause ) )  (in a Data Set expression) 5719 
median  ( component over ( analyticClause ) ) (in a Component expression within a calc clause) 5720 
 5721 
170 
 
Input parameters 5722 
dataset  the operand Data Set 5723 
component  the operand Component 5724 
groupingClause see Aggregate invocation  5725 
analyticClause see Analytic invocation 5726 
 5727 
Examples of valid syntaxes 5728 
See Aggregate and Analytic invocations above, at the beginning of the section. 5729 
 5730 
Semantics for scalar operations 5731 
This operator cannot be applied to scalar values.  5732 
 5733 
Input parameters type 5734 
dataset ::                dataset {measure<number>_+} 5735 
component ::       component<number> 5736 
 5737 
Result type 5738 
result ::     dataset   { measure<number>  _+  }   5739 
 |  component<number> 5740 
 5741 
Additional constraints 5742 
None.  5743 
 5744 
Behaviour 5745 
The operator returns the median value of the input values. 5746 
For other details, see Aggregate and Analytic invocations. 5747 
 5748 
Examples 5749 
Given the Data Set DS_1: 5750 
 5751 
DS_1 
Id_1 Id_2 Id_3 Me_1 
2011 A XX 3 
2011 A YY 5 
2011 B YY 7 
2012 A XX 2 
2012 B YY 4 
 5752 
 5753 
Example 1: DS_r := median ( DS_1  group by  Id_1  )  results in: 5754 
 5755 
DS_r 
Id_1 Me_1 
2011 5 
2012 3 
Sum :  sum 5756 
Aggregate syntax 5757 
sum  ( dataset { groupingClause } )   (in a Data Set expression) 5758 
sum  ( component  ) { groupingClause }  (in a Component expression within an aggr clause)  5759 
 5760 
171 
 
Analytic syntax 5761 
sum  ( dataset  over ( analyticClause ) )  (in a Data Set expression) 5762 
sum  ( component  over ( analyticClause ) )  (in a Component expression within a calc clause) 5763 
 5764 
Input parameters 5765 
dataset  the operand Data Set 5766 
component  the operand Component 5767 
groupingClause see Aggregate invocation  5768 
analyticClause see Analytic invocation 5769 
 5770 
Examples of valid syntaxes 5771 
See Aggregate and Analytic invocations above, at the beginning of the section. 5772 
 5773 
Semantics for scalar operations 5774 
This operator cannot be applied to scalar values.  5775 
 5776 
Input parameters type 5777 
dataset ::              dataset { measure<number> _+ } 5778 
component ::  component<number> 5779 
 5780 
Result type 5781 
result ::  dataset   { measure<number>  _+  }   5782 
 |  component<number> 5783 
 5784 
Additional constraints 5785 
None.  5786 
 5787 
Behaviour 5788 
The operator returns the sum of the input values. 5789 
For other details, see Aggregate and Analytic invocations. 5790 
 5791 
Examples 5792 
Given the Data Set DS_1 : 5793 
 5794 
DS_1 
Id_1 Id_2 Id_3 Me_1 
2011 A XX 3 
2011 A YY 5 
2011 B YY 7 
2012 A XX 2 
2012 B YY 4 
 5795 
Example 1: DS_r := sum ( DS_1 group by  Id_1  )  results in: 5796 
 5797 
DS_r 
Id_1 Me_1 
2011 15 
2012 6 
 5798 
172 
 
Average value :  avg 5799 
Aggregate syntax 5800 
avg  ( dataset { groupingClause } )   (in a Data Set expression) 5801 
avg  ( component )  { groupingClause }    (in a Component expression within an aggr clause)  5802 
 5803 
Analytic syntax 5804 
avg  ( dataset  over ( analyticClause ) )  (in a Data Set expression) 5805 
avg  ( component  over ( analyticClause ) )  (in a Component expression within a calc clause) 5806 
 5807 
Input parameters 5808 
dataset  the operand Data Set 5809 
component  the operand Component 5810 
groupingClause see Aggregate invocation  5811 
analyticClause see Analytic invocation 5812 
 5813 
Examples of valid syntaxes 5814 
See Aggregate and Analytic invocations above, at the beginning of the section. 5815 
 5816 
Semantics for scalar operations 5817 
This operator cannot be applied to scalar values.  5818 
 5819 
Input parameters type 5820 
dataset ::                dataset {measure<number> _+} 5821 
component ::  component<number> 5822 
 5823 
Result type 5824 
result ::  dataset   { measure<number>  _+  }   5825 
 |  component<number> 5826 
Additional constraints 5827 
None. 5828 
 5829 
Behaviour 5830 
The operator returns the mean of the input values. 5831 
For other details, see Aggregate and Analytic invocations. 5832 
 5833 
Examples 5834 
Given the Data Set DS_1: 5835 
 5836 
DS_1 
Id_1 Id_2 Id_3 Me_1 
2011 A XX 3 
2011 A YY 5 
2011 B YY 7 
2012 A XX 2 
2012 B YY 4 
 5837 
Example 1: DS_r := avg ( DS_1 group by  Id_1  )  results in: 5838 
 5839 
DS_r 
Id_1 Me_1 
2011 5 
173 
 
2012 3 
 5840 
Population standard deviation :  stddev_pop 5841 
Aggregate syntax 5842 
stddev_pop  ( dataset { groupingClause } )  (in a Data Set expression) 5843 
stddev_pop  ( component  ) { groupingClause }  (in a Component expression within an aggr clause)  5844 
 5845 
Analytic syntax 5846 
stddev_pop  ( dataset over ( analyticClause ) ) (in a Data Set expression) 5847 
stddev_pop  ( component over ( analyticClause ) ) (in a Component expression within a calc clause) 5848 
 5849 
Input parameters 5850 
dataset  the operand Data Set 5851 
component  the operand Component 5852 
groupingClause see Aggregate invocation  5853 
analyticClause see Analytic invocation 5854 
 5855 
Examples of valid syntaxes 5856 
See Aggregate and Analytic invocations above, at the beginning of the section. 5857 
 5858 
Semantics for scalar operations 5859 
This operator cannot be applied to scalar values.  5860 
 5861 
Input parameters type 5862 
dataset ::              dataset { measure<number> _+ } 5863 
component ::  component<number> 5864 
 5865 
Result type 5866 
result ::  dataset   { measure<number>   _+  }   5867 
 |  component<number> 5868 
 5869 
Additional constraints 5870 
None. 5871 
 5872 
Behaviour 5873 
The operator returns the “population standard deviation” of the input values. 5874 
For other details, see Aggregate and Analytic invocations. 5875 
 5876 
Examples 5877 
 5878 
Given the Data Set DS_1: 5879 
 5880 
DS_1 
Id_1 Id_2 Id_3 Me_1 
2011 A XX 3 
2011 A YY 5 
2011 B YY 7 
2012 A XX 2 
2012 B YY 4 
 5881 
Example 1: DS_r := stddev_pop ( DS_1 group by  Id_1  )  results in: 5882 
174 
 
 5883 
DS_r 
Id_1 Me_1 
2011 1.633 
2012 1 
 5884 
Sample standard deviation :  stddev_samp 5885 
Aggregate syntax 5886 
stddev_samp  ( dataset { groupingClause } )  (in a Data Set expression) 5887 
stddev_samp  ( component ) { groupingClause }  (in a Component expr. within an aggr clause)  5888 
 5889 
Analytic syntax 5890 
stddev_samp  ( dataset over ( analyticClause ) )  (in a Data Set expression) 5891 
stddev_samp  ( component over ( analyticClause ) ) (in a Component expr. within a calc clause) 5892 
 5893 
Input parameters 5894 
dataset  the operand Data Set 5895 
component  the operand Component 5896 
groupingClause see Aggregate invocation  5897 
analyticClause see Analytic invocation 5898 
 5899 
Semantics for scalar operations 5900 
This operator cannot be applied to scalar values.  5901 
 5902 
Examples of valid syntaxes 5903 
See Aggregate and Analytic invocations above, at the beginning of the section. 5904 
 5905 
Input parameters type 5906 
dataset ::              dataset { measure<number> _+ } 5907 
component ::  component<number> 5908 
 5909 
Result type 5910 
result ::  dataset   { measure<number>  _+  }   5911 
|  component<number> 5912 
 5913 
Additional constraints 5914 
None. 5915 
 5916 
Behaviour 5917 
The operator returns the “sample standard deviation” of the input values. 5918 
For other details, see Aggregate and Analytic invocations. 5919 
 5920 
Examples 5921 
Given the Data Set DS_1: 5922 
 5923 
DS_1 
Id_1 Id_2 Id_3 Me_1 
2011 A XX 3 
2011 A YY 5 
175 
 
2011 B YY 7 
2012 A XX 2 
2012 B YY 4 
 5924 
Example 1: DS_r := stddev_samp ( DS_1 group by  Id_1  )  results in: 5925 
 5926 
DS_r 
Id_1 Me_1 
2011 2 
2012 1.4142 
 5927 
Population variance :  var_pop 5928 
Aggregate syntax 5929 
var_pop  ( dataset { groupingClause } )  (in a Data Set expression) 5930 
var_pop  ( component  ) { groupingClause }  (in a Component expression within an aggr clause)  5931 
 5932 
Analytic syntax 5933 
var_pop  ( dataset  over ( analyticClause ) )  (in a Data Set expression) 5934 
var_pop  ( component  over ( analyticClause ) ) (in a Component expression within a calc clause) 5935 
 5936 
Input parameters 5937 
dataset  the operand Data Set 5938 
component  the operand Component 5939 
groupingClause see Aggregate invocation  5940 
analyticClause see Analytic invocation 5941 
 5942 
Examples of valid syntaxes 5943 
See Aggregate and Analytic invocations above, at the beginning of the section. 5944 
 5945 
Semantics for scalar operations 5946 
This operator cannot be applied to scalar values.  5947 
 5948 
Input parameters type 5949 
dataset ::              dataset {measure<number>_+} 5950 
component ::  component<number> 5951 
 5952 
Result type 5953 
result ::  dataset   { measure<number>  _+  }   5954 
 |  component<number> 5955 
 5956 
Additional constraints 5957 
None. 5958 
 5959 
Behaviour 5960 
The operator returns the “population variance” of the input values. 5961 
For other details, see Aggregate and Analytic invocations. 5962 
 5963 
Examples 5964 
Given the Data Set DS_1 : 5965 
 5966 
176 
 
DS_1 
Id_1 Id_2 Id_3 Me_1 
2011 A XX 3 
2011 A YY 5 
2011 B YY 7 
2012 A XX 2 
2012 B YY 4 
 5967 
Example 1: DS_r := var_pop ( DS_1 group by  Id_1  )  results in: 5968 
 5969 
DS_r 
Id_1 Me_1 
2011 2,6667 
2012 1 
Sample variance :  var_samp 5970 
Aggregate syntax 5971 
var_samp  ( dataset { groupingClause } )  (in a Data Set expression) 5972 
var_samp  ( component  ) { groupingClause } (in a Component expression within an aggr clause)  5973 
 5974 
Analytic syntax 5975 
var_samp  ( dataset over ( analyticClause ) ) (in a Data Set expression) 5976 
var_samp  ( component over ( analyticClause ) ) (in a Component expression within a calc clause) 5977 
 5978 
Input parameters 5979 
dataset  the operand Data Set 5980 
component  the operand Component 5981 
groupingClause see Aggregate invocation  5982 
analyticClause see Analytic invocation 5983 
 5984 
Examples of valid syntaxes 5985 
See Aggregate and Analytic invocations above, at the beginning of the section. 5986 
 5987 
Semantics for scalar operations 5988 
This operator cannot be applied to scalar values.  5989 
 5990 
Input parameters type 5991 
dataset ::              dataset {measure<number>_+} 5992 
component ::  component<number> 5993 
 5994 
Result type 5995 
result ::  dataset   { measure<number>  _+  }   5996 
 |  component<number> 5997 
 5998 
Additional constraints 5999 
None. 6000 
 6001 
Behaviour 6002 
The operator returns the sample variance of the input values. 6003 
177 
 
For other details, see Aggregate and Analytic invocations. 6004 
 6005 
Examples 6006 
 6007 
Given the Data Set DS_1 6008 
 6009 
DS_1 
Id_1 Id_2 Id_3 Me_1 
2011 A XX 3 
2011 A YY 5 
2011 B YY 7 
2012 A XX 2 
2012 B YY 4 
 6010 
Example 1: DS_r := var_samp ( DS_1 group by [ Id_1 ] )  results in: 6011 
 6012 
DS_r 
Id_1 Me_1 
2011 4 
2012 2 
 6013 
First value : first_value 6014 
Syntax 6015 
first_value  ( dataset  over ( analyticClause ) )  (in a Data Set expression) 6016 
first_value  ( component  over ( analyticClause ) ) (in a Component expression within a calc clause) 6017 
 6018 
Input parameters 6019 
dataset  the operand Data Set 6020 
component  the operand Component 6021 
analyticClause see Analytic invocation 6022 
 6023 
Examples of valid syntaxes 6024 
See Analytic invocation above, at the beginning of the section. 6025 
 6026 
Semantics for scalar operations 6027 
This operator cannot be applied to scalar values.  6028 
 6029 
Input parameters type 6030 
dataset ::              dataset { measure<scalar> _+ } 6031 
component ::  component<scalar> 6032 
 6033 
Result type 6034 
result ::  dataset   6035 
 |  component<scalar> 6036 
 6037 
Additional constraints 6038 
The Aggregate invocation is not allowed. 6039 
 6040 
178 
 
Behaviour 6041 
The operator returns the first value (in the value order) of the set of Data Points that belong to the same analytic 6042 
window as the current Data Point.  6043 
When invoked at Data Set level, it returns the first value for each Measure of the input Data Set. The first value of 6044 
different Measures can result from different Data Points. 6045 
When invoked at Component level, it returns the first value of the specified Component. 6046 
For other details, see Analytic invocation. 6047 
 6048 
Examples 6049 
Given the Data Set DS_1 : 6050 
 6051 
DS_1 
Id_1 Id_2 Id_3 Me_1 Me_2 
A XX 1993 3 1 
A XX 1994 4 9 
A XX 1995 7 5 
A XX 1996 6 8 
A YY 1993 9 3 
A YY 1994 5 4 
A YY 1995 10 2 
A YY 1996 2 7 
 6052 
Example 1:  6053 
 6054 
DS_r := first_value ( DS_1 over ( partition by  Id_1, Id_2 order by  Id_3  data points between 1 preceding and 6055 
1 following) )   6056 
 6057 
results in: 6058 
 6059 
DS_r 
Id_1 Id_2 Id_3 Me_1 Me_2 
A XX 1993 3 1 
A XX 1994 3 1 
A XX 1995 4 5 
A XX 1996 6 5 
A YY 1993 5 3 
A YY 1994 5 2 
A YY 1995 2 2 
A YY 1996 2 2 
 6060 
Last value : last_value 6061 
Syntax 6062 
last_value  ( dataset  over ( analyticClause ) )  (in a Data Set expression) 6063 
last_value  ( component  over ( analyticClause ) ) (in a Component expression within a calc clause) 6064 
 6065 
Input parameters 6066 
dataset  the operand Data Set 6067 
179 
 
component  the operand Component 6068 
analyticClause see Analytic invocation 6069 
 6070 
Examples of valid syntaxes 6071 
See Analytic invocation above, at the beginning of the section. 6072 
 6073 
Semantics for scalar operations 6074 
This operator cannot be applied to scalar values.  6075 
 6076 
Input parameters type 6077 
dataset ::              dataset {measure<scalar> _+} 6078 
component ::  component<scalar> 6079 
 6080 
Result type 6081 
result ::  dataset   6082 
 |  component<scalar> 6083 
 6084 
Additional constraints 6085 
The Aggregate invocation is not allowed. 6086 
 6087 
Behaviour 6088 
The operator returns the last value (in the value order) of the set of Data Points that belong to the same analytic 6089 
window as the current Data Point.  6090 
When invoked at Data Set level, it returns the last value for each Measure of the input Data Set. The last value of 6091 
different Measures can result from different Data Points. 6092 
When invoked at Component level, it returns the last value of the speficied Component. 6093 
For other details, see Analytic invocation. 6094 
 6095 
Examples 6096 
 6097 
Given the Data Set DS_1: 6098 
 6099 
DS_1 
Id_1 Id_2 Id_3 Me_1 Me_2 
A XX 1993 3 1 
A XX 1994 4 9 
A XX 1995 7 5 
A XX 1996 6 8 
A YY 1993 9 3 
A YY 1994 5 4 
A YY 1995 10 2 
A YY 1996 2 7 
 6100 
 6101 
Example 1:  6102 
 6103 
DS_r := last_value ( DS_1 over ( partition by  Id_1, Id_2 order by  Id_3  data points between 1 preceding and 6104 
1 following ) )   6105 
 6106 
results in: 6107 
 6108 
DS_r 
Id_1 Id_2 Id_3 Me_1 Me_2 
A XX 1993 4 9 
180 
 
A XX 1994 7 9 
A XX 1995 7 9 
A XX 1996 7 8 
A YY 1993 9 4 
A YY 1994 10 4 
A YY 1995 10 7 
A YY 1996 10 7 
 6109 
Lag :  lag 6110 
Syntax 6111 
 6112 
in a Data Set expression: 6113 
lag  ( dataset {, offset {, defaultValue } } over ( { partitionClause } orderClause) )  6114 
 6115 
In a Component expression within a calc clause: 6116 
lag  ( component {, offset  {, defaultValue } } over ( { partitionClause } orderClause ) ) 6117 
  6118 
Input parameters 6119 
dataset  the operand Data Set 6120 
component  the operand Component 6121 
offset the relative position prior to the current Data Point  6122 
defaultValue the value returned when the offset goes outside of the partition.  6123 
partitionClause see Analytic invocation 6124 
orderClause see Analytic invocation 6125 
 6126 
Examples of valid syntaxes 6127 
See Analytic invocation above, at the beginning of the section. 6128 
 6129 
Semantics for scalar operations 6130 
This operator cannot be applied to scalar values.  6131 
 6132 
Input parameters type 6133 
dataset ::              dataset  6134 
component ::  component 6135 
offset :: integer [ value > 0 ] 6136 
default value :: scalar 6137 
 6138 
Result type 6139 
result ::  dataset   6140 
 |  component 6141 
 6142 
Additional constraints 6143 
The Aggregate invocation is not allowed. 6144 
The windowClause of the Analytic invocation syntax is not allowed. 6145 
 6146 
Behaviour 6147 
In the ordered set of Data Points of the current partition, the operator returns the value(s) taken from the Data 6148 
Point at the specified  physical offset prior to the current Data Point.  6149 
If defaultValue is not specified then the value returned when the offset goes outside the partition is NULL. 6150 
For other details, see Analytic invocation. 6151 
 6152 
Examples 6153 
Given the Data Set DS_1 : 6154 
 6155 
181 
 
DS_1 
Id_1 Id_2 Id_3 Me_1 Me_2 
A XX 1993 3 1 
A XX 1994 4 9 
A XX 1995 7 5 
A XX 1996 6 8 
A YY 1993 9 3 
A YY 1994 5 4 
A YY 1995 10 2 
A YY 1996 2 7 
 6156 
 6157 
Example 1: DS_r := lag ( DS_1 , 1 over ( partition by  Id_1 , Id_2  order by  Id_3  ) )   results in: 6158 
 6159 
DS_r 
Id_1 Id_2 Id_3 Me_1 Me_2 
A XX 1993 NULL NULL 
A XX 1994 3 1 
A XX 1995 4 9 
A XX 1996 7 5 
A YY 1993 NULL NULL 
A YY 1994 9 3 
A YY 1995 5 4 
A YY 1996 10 2 
 6160 
lead :  lead 6161 
Syntax 6162 
 6163 
in a Data Set expression: 6164 
lead  ( dataset , {offset  {, defaultValue } } over ( { partitionClause } orderClause ) )   6165 
 6166 
in a Component expression within a calc clause: 6167 
lead  ( component , {offset  {, defaultValue } } over ( { partitionClause } orderClause ) )  6168 
 6169 
Input parameters 6170 
dataset  the operand Data Set 6171 
component  the operand Component 6172 
offset the relative position beyond the current Data Point  6173 
defaultValue the value returned when the offset goes outide the partition.  6174 
partitionClause see Analytic invocation 6175 
orderClause see Analytic invocation 6176 
 6177 
Examples of valid syntaxes 6178 
See Analytic invocation above, at the beginning of the section. 6179 
 6180 
Semantics for scalar operations 6181 
This operator cannot be applied to scalar values.  6182 
 6183 
182 
 
Input parameters type 6184 
dataset ::              dataset  6185 
component ::  component 6186 
offset :: integer [ value > 0 ] 6187 
default value :: scalar 6188 
 6189 
Result type 6190 
result ::  dataset   6191 
 |  component 6192 
 6193 
Additional constraints 6194 
The Aggregate invocation is not allowed. 6195 
The windowClause of the Analytic invocation syntax is not allowed. 6196 
 6197 
Behaviour 6198 
In the ordered set of Data Points of the current partition, the operator returns the value(s) taken from the Data 6199 
Point at the specified physical offset beyond the current Data Point. 6200 
If defaultValue is not specified, then the value returned when the offset goes outside the partition is NULL. 6201 
For other details, see Analytic invocation. 6202 
 6203 
Examples 6204 
Given the Data Set DS_1 6205 
 6206 
DS_1 
Id_1 Id_2 Id_3 Me_1 Me_2 
A XX 1993 3 1 
A XX 1994 4 9 
A XX 1995 7 5 
A XX 1996 6 8 
A YY 1993 9 3 
A YY 1994 5 4 
A YY 1995 10 2 
A YY 1996 2 7 
 6207 
Example 1: DS_r := lead ( DS_1 , 1 over ( partition by  Id_1 , Id_2 order by  Id_3  ) )   results in: 6208 
 6209 
DS_r 
Id_1 Id_2 Id_3 Me_1 Me_2 
A XX 1993 4 9 
A XX 1994 7 5 
A XX 1995 6 8 
A XX 1996 NULL NULL 
A YY 1993 5 4 
A YY 1994 10 2 
A YY 1995 2 7 
A YY 1996 NULL NULL 
 6210 
183 
 
Rank :  rank 6211 
Syntax 6212 
rank  ( over ( { partitionClause } orderClause ) )  (in a Component expression within a calc clause) 6213 
 6214 
Input parameters 6215 
partitionClause see Analytic invocation 6216 
orderClause see Analytic invocation 6217 
 6218 
Examples of valid syntaxes 6219 
See Analytic invocation above, at the beginning of the section. 6220 
 6221 
Semantics for scalar operations 6222 
This operator cannot be applied to scalar values.  6223 
 6224 
Input parameters type 6225 
dataset ::              dataset 6226 
component ::  component 6227 
 6228 
Result type 6229 
result ::  dataset   { measure<integer>  int_var  }   6230 
 |  component<integer> 6231 
 6232 
Additional constraints 6233 
The invocation at Data Set level is not allowed. 6234 
The Aggregate invocation is not allowed. 6235 
The windowClause of the Analytic invocation syntax is not allowed. 6236 
 6237 
Behaviour 6238 
The operator returns an order number (rank) for each Data Point, starting from the number 1 and following the order 6239 
specified in the orderClause.  If some Data Points are in the same order according to the specified orderClause, the 6240 
same order number (rank) is assigned and a gap appears in the sequence of the assigned ranks (for example, if four Data 6241 
Points have the same rank 5, the following assigned rank would be 9). 6242 
For other details, see Analytic invocation. 6243 
 6244 
Examples 6245 
Given the Data Set DS_1: 6246 
 6247 
DS_1 
Id_1 Id_2 Id_3 Me_1 Me_2 
A XX 2000 3 1 
A XX 2001 4 9 
A XX 2002 7 5 
A XX 2003 6 8 
A YY 2000 9 3 
A YY 2001 5 4 
A YY 2002 10 2 
A YY 2003 5 7 
 6248 
 6249 
Example 1:  6250 
 6251 
DS_r := DS_1 [ calc Me2 := rank ( over ( partition by  Id_1 , Id_2  order by  Me_1  ) )  results in: 6252 
 6253 
184 
 
DS_r 
Id_1 Id_2 Id_3 Me_1 Me_2 
A XX 2000 3 1 
A XX 2001 4 2 
A XX 2002 7 4 
A XX 2003 6 3 
A YY 2000 9 3 
A YY 2001 5 1 
A YY 2002 10 4 
A YY 2003 5 1 
 6254 
Ratio to report :  ratio_to_report 6255 
Syntax 6256 
ratio_to_report  ( dataset  over ( partitionClause ) )  (in a Data Set expression) 6257 
ratio_to_report  ( component over ( partitionClause ) )  (in a Component expr. within a calc clause) 6258 
 6259 
Input parameters 6260 
dataset the operand Data Set 6261 
component the operand Component 6262 
partitionClause see Analytic invocation 6263 
 6264 
Examples of valid syntaxes 6265 
See Analytic invocation above, at the beginning of the section. 6266 
 6267 
Semantics for scalar operations 6268 
This operator cannot be applied to scalar values.  6269 
 6270 
Input parameters type 6271 
dataset ::              dataset { measure<number>_+ } 6272 
component :: component<number> 6273 
 6274 
Result type 6275 
result ::  dataset   { measure<number>  _+  }   6276 
 |  component<number> 6277 
 6278 
Additional constraints 6279 
The Aggregate invocation is not allowed. 6280 
The orderClause and windowClause of the Analytic invocation syntax are not allowed. 6281 
 6282 
Behaviour 6283 
The operator returns the ratio between the value of the current Data Point and the sum of the values of the 6284 
partition which the current Data Point belongs to. 6285 
For other details, see Analytic invocation. 6286 
 6287 
Examples 6288 
Given the Data Set DS_1: 6289 
 6290 
DS_1 
Id_1 Id_2 Id_3 Me_1 Me_2 
A XX 2000 3 1 
185 
 
A XX 2001 4 3 
A XX 2002 7 5 
A XX 2003 6 1 
A YY 2000 12 0 
A YY 2001 8 8 
A YY 2002 6 5 
A YY 2003 14 -3 
 6291 
 6292 
Example 1: DS_r := ratio_to_report ( DS_1  over ( partition by  Id_1, Id_2  ) )  results in: 6293 
 6294 
DS_r 
Id_1 Id_2 Id_3 Me_1 Me_2 
A XX 2000 0.15 0,1 
A XX 2001 0.2 0.3 
A XX 2002 0.35 0.5 
A XX 2003 0.3 0.1 
A YY 2000 0.3 0 
A YY 2001 0.2 0.8 
A YY 2002 0.15 0.5 
A YY 2003 0.35 -0.3 
 6295 
186 
 
VTL-ML  -  Data validation operators 6296 
check_datapoint  6297 
Syntax 6298 
check_datapoint ( op , dpr { components listComp } { output output } ) 6299 
listComp ::= comp { , comp }* 6300 
output ::=  invalid | all | all_measures 6301 
Input parameters 6302 
op  the Data Set to check 6303 
dpr  the Data Point Ruleset to be used  6304 
listComp  if dpr is defined on Value Domains then listComp is the list of Components of op to be 6305 
associated (in positional order) to the conditioning Value Domains defined in dpr. If dpr is 6306 
defined on Variables then listComp is the list of Components of op to be associated (in 6307 
positional order) to the conditioning Variables defined in dpr (for documentation purposes). 6308 
comp Component of op 6309 
output specifies the Data Points and the Measures of the resulting Data Set: 6310 
invalid the resulting Data Set contains a Data Point for each Data Point of op and 6311 
each Rule in dpr that evaluates to FALSE on that Data Point. The resulting 6312 
Data Set has the Measures of op. 6313 
all  the resulting Data Set contains a data point for each Data Point of op and 6314 
each Rule in dpr. The resulting Data Set has the boolean Measure bool_var. 6315 
all_measures the resulting Data Set contains a Data Point for each Data Point of op and 6316 
each Rule in dpr. The resulting dataset has the Measures of op and the 6317 
boolean Measure bool_var. 6318 
If not specified then output is assumed to be invalid. See the Behaviour for further details. 6319 
Examples of valid syntaxes 6320 
check_datapoint ( DS1, DPR invalid ) 6321 
check_datapoint ( DS1, DPR all_measures ) 6322 
 6323 
Semantics for scalar operations 6324 
This operator cannot be applied to scalar values.  6325 
 6326 
Input parameters type: 6327 
op :: dataset 6328 
dpr ::  name < datapoint > 6329 
comp ::  name < component > 6330 
 6331 
Result type: 6332 
result :: dataset 6333 
 6334 
Additional constraints 6335 
If dpr is defined on Value Domains then it is mandatory to specify listComp. The Components specified in  6336 
listComp must belong to the operand op and be defined on the Value Domains specified in the signature of dpr. 6337 
If dpr is defined on Variables then the Components specified in the signature of dpr must belong to the operand 6338 
op. 6339 
If dpr is defined on Variables and listComp is specified then the Components specified in listComp are the same, 6340 
in the same order, as those specified in op (they are provided for documentation purposes). 6341 
 6342 
187 
 
Behaviour 6343 
It returns a Data Set having the following Components: 6344 
 the Identifier Components of op 6345 
 the Identifier Component ruleid whose aim is to identify the Rule that has generated the actual Data 6346 
Point (it contains at least the Rule name specified in dpr 8) 6347 
 if the output parameter is invalid: the original Measures of op (no boolean measure) 6348 
 if the output parameter is all: the boolean Measure bool_var  whose value is the result of the evaluation 6349 
of a rule on a Data Point (TRUE, FALSE or NULL). 6350 
 if the output parameter is all_measures: the original measures of op and the boolean Measure bool_var 6351 
whose value is the result of the evaluation of a rule on a Data Point (TRUE, FALSE or NULL). 6352 
 the Measure errorcode that contains the errorcode specified in the rule 6353 
 the Measure errorlevel that contains the errorlevel specified in the rule 6354 
 6355 
A Data Point of op can produce several Data Points in the resulting Data Set, each of them with a different value 6356 
of ruleid. If output is invalid then the resulting Data Set contains a Data Point for each Data Point of op and each 6357 
rule of dpr that evaluates to FALSE. If output is all or all_measures then the resulting Data Set contains a Data 6358 
Point for each Data Point of op and each rule of dpr. 6359 
Examples 6360 
define datapoint ruleset dpr1 ( variable Id_3, Me_1 ) is 6361 
   when Id_3 = “CREDIT” then Me_1 >= 0 errorcode “Bad credit” 6362 
 ; when Id_3 = “DEBIT” then Me_1 >= 0 errorcode “Bad debit” 6363 
end datapoint ruleset 6364 
 6365 
Given the Data Set DS_1: 6366 
 6367 
DS_1 
Id_1 Id_2 Id_3 Me_1 
2011 I CREDIT 10 
2011 I DEBIT -2 
2012 I CREDIT 10 
2012 I DEBIT 2 
 6368 
DS_r := check_datapoint ( DS_1, dpr1 )  results in: 6369 
 6370 
DS_r 
Id_1 Id_2 Id_3 ruleid obs_value errorcode errorlevel 
2011 I DEBIT dpr1_2 -2 Bad debit  
 6371 
 6372 
DS_r := check_datapoint ( DS_1, dpr1 all )  results in: 6373 
 6374 
DS_r 
Id_1 Id_2 Id_3 ruleid bool_var errorcode errorlevel 
2011 I CREDIT dpr1_1 true   
2011 I CREDIT dpr1_2 true   
2011 I DEBIT dpr1_1 true   
                                                           
8 The content of ruleid maybe personalised in the implementation 
188 
 
2011 I DEBIT dpr1_2 false Bad debit  
2012 I CREDIT dpr1_1 true   
2012 I CREDIT dpr1_2 true   
2012 I DEBIT dpr1_1 true   
2012 I DEBIT dpr1_2 true   
 6375 
check_hierarchy 6376 
Syntax 6377 
check_hierarchy ( op , hr { condition condComp { , condComp }* } { rule ruleComp }  6378 
       { mode } { input } { output } ) 6379 
mode ::=  non_null | non_zero | partial_null | partial_zero | always_null | always_zero  6380 
input ::=  dataset | dataset_priority  6381 
output ::=  invalid | all | all_measures 6382 
 6383 
 6384 
Input parameters 6385 
op  the Data Set to be checked 6386 
hr  the hierarchical Ruleset to be used 6387 
condComp  condComp is a Component of op to be associated (in positional order) to the conditioning 6388 
Value Domains or Variables defined in hr (if any). 6389 
ruleComp ruleComp is the Identifier of op to be associated to the rule Value Domain or Variable defined 6390 
in hr. 6391 
mode this parameter specifies how to treat the possible missing Data Points corresponding to the 6392 
Code Items in the left and right sides of the rules and which Data Points are produced in 6393 
output. The meaning of the possible values of the parameter is explained below. 6394 
input this parameter specifies the source of the values used as input of the comparisons. The 6395 
meaning of the possible values of the parameter is explained below. 6396 
output this parameter specifies the structure and the content of the resulting dataset. The meaning of 6397 
the possible values of the parameter is explained below. 6398 
 6399 
Examples of valid syntaxes 6400 
check_hierarchy ( DS1, HR_2  non_null  dataset  invalid )    6401 
check_hierarchy ( DS1, HR_3  non_zero dataset_priority  all ) 6402 
 6403 
Input parameters type 6404 
op ::  dataset { measure<number> _  }  6405 
hr ::  name <  hierarchical >  6406 
condComp ::  name < component > 6407 
ruleComp ::  name < identifier > 6408 
 6409 
Result type 6410 
result ::   dataset {measure<number> _  }     6411 
 6412 
Additional constraints 6413 
If hr is defined on Value Domains then it is mandatory to specify the condition (if any in the ruleset hr) and the 6414 
rule parameters. Moreover, the Components specified as condComp and ruleComp must belong to the operand 6415 
189 
 
op and must take values on the Value Domains corresponding, in positional order, to the ones specified in the 6416 
condition and rule parameter of hr. 6417 
If hr is defined on Variables, the specification of condComp and ruleComp is not needed, but they can be 6418 
specified all the same if it is desired to show explicitly in the invocation which are the involved Components: in 6419 
this case, the condComp and ruleComp  must be the same and in the same order as the Variables specified in in 6420 
the condition and rule signatures of hr.  6421 
 6422 
 6423 
Behaviour 6424 
 6425 
The check_hierarchy operator applies the Rules of the Ruleset hr to check the Code Items Relations between 6426 
the Code Items present in op (as for the Code Items Relations, see the User Manual - section “Generic Model for 6427 
Variables and Value Domains”). The operator checks if the relation between the left and the right member is 6428 
fulfilled, giving TRUE in positive case and FALSE in negative case. 6429 
 6430 
The Attribute propagation rule is applied on each group of Data Points which contributes to the same Data Point 6431 
of the result.  6432 
 6433 
The behaviours relevanto to the different options of the input parameters are the following. 6434 
First, the parameter input is used to determine the source of the Data Points used as input of the 6435 
check_hierarchy. The possible options of the parameter input and the corresponding behaviours are the 6436 
following: 6437 
dataset  this option addresses the case where all the input Data Points of all the Rules of the Ruleset are 6438 
expected to be taken from the input Data Set (the operand op).  6439 
 For each Rule of the Ruleset and for each item on the left and right sides of the Rule, the 6440 
operator takes the input Data Points exclusively from the operand op.  6441 
dataset_prority this option addresses the case where the input Data Points of all the Rules of the Ruleset are 6442 
preferably taken from the input Data Set (the operand op), however if a valid Measure value 6443 
for an expected Data Point is not found in op, the attempt is made to take it from the computed 6444 
output of a (possible) other Rule.  6445 
 For each Rule of the Ruleset and for each item on the left and right sides of the Rule:  6446 
 if the item is not defined as the result (left side) of another Rule that applies the Code Item 6447 
relation “is equal to” (=), the current Rule takes the input Data Points from the operand 6448 
op.  6449 
 if the item is defined as result of another Rule R that applies the Code Item relation “is 6450 
equal to” (=), then: 6451 
o if an expected input Data Point exists in op and its Measure is not NULL, then the 6452 
current Rule takes such Data Point from op;  6453 
o if an expected input Data Point does not exist in op or its measure is NULL, then 6454 
the current Rule takes the Data Point (if any) that has the same Identifiers’ values 6455 
from the computed output of the other Rule R;  6456 
if the parameter input is not specified then it is assumed to be dataset. 6457 
Then the parameter mode is considered, to determine the behaviour for missing Data Points and for the Data 6458 
Points to be produced in the output. The possible options of the parameter mode and the corresponding 6459 
behaviours are the following: 6460 
non_null the result Data Point is produced when all the items involved in the comparison exist and have 6461 
not NULL Measure value (i.e., when no Data Point corresponding to the Code Items of the left 6462 
and right sides of the rule is missing or has NULL Measure value); under this option, in 6463 
evaluating the comparison, the possible missing Data Points corresponding to the Code Items 6464 
of the left and right sides of the rule are considered existing and having a NULL Measure value;  6465 
non_zero the result Data Point is produced when at least one of the items involved in the comparison 6466 
exist and have Measure not equal to 0 (zero); the possible missing Data Points corresponding 6467 
to the Code Items of the left and right sides of the rule are considered existing and having a 6468 
Measure value equal to 0;  6469 
partial_null the result Data Point is produced if at least one Data Point corresponding to the Code Items of 6470 
the left and right sides of the rule is found (whichever is its Measure value); the possible 6471 
190 
 
missing Data Points corresponding to the Code Items of the left and right sides of the rule are 6472 
considered existing and having a NULL Measure value;  6473 
partial_zero the result Data Point is produced if at least one Data Point corresponding to the Code Items of 6474 
the left and right sides of the rule is found (whichever is its Measure value); the possible 6475 
missing Data Points corresponding to the Code Items of the left and right sides of the rule are 6476 
considered existing and having a Measure value equal to 0 (zero); 6477 
always_null the result Data Point is produced in any case; the possible missing Data Points corresponding 6478 
to the Code Items of the left and right sides of the rule are considered existing and having a 6479 
Measure value equal to NULL;  6480 
always_zero the result Data Point is produced in any case; the possible missing Data Points corresponding 6481 
to the Code Items of the left and right sides of the rule are considered existing and having a 6482 
Measure value equal to 0 (zero); 6483 
If the parameter mode is not specified, then it is assumed to be non_null. 6484 
The following table summarizes the behaviour of the options of the parameter “mode” 6485 
 6486 
OPTION of the 
MODE 
PARAMETER: 
Missing Data 
Points are 
considered: 
Null Data 
Points are 
considered: 
Condition for 
evaluating the rule 
Returned Data 
Points 
Non_null NULL NULL If all the involved Data 
Points are not NULL 
Only not NULL 
Data Points (Zeros 
are returned too) 
Non_zero Zero NULL 
If at least one of the 
involved Data Points is 
<> zero 
Only not zero Data 
Points  (NULLS are 
returned too) 
Partial_null NULL NULL 
If at least one of the 
involved  Data Points 
is not NULL 
Data Points of any 
value (NULL, not 
NULL and zero too) 
Partial_zero Zero NULL 
If at least one of the 
involved  Data Points 
is not NULL 
Data Points of any 
value (NULL, not 
NULL and zero too) 
Always_null NULL NULL Always 
Data Points of any 
value (NULL, not 
NULL and zero too) 
Always_zero Zero NULL Always 
Data Points of any 
value (NULL, not 
NULL and zero too) 
 6487 
Finally the parameter output is considered, to determine the structure and content of the resulting Data Set. The 6488 
possible options of the parameter output and the corresponding behaviours are the following: 6489 
all all the Data Points produced by the comparison are returned, both the valid ones (TRUE) and 6490 
the invalid ones (FALSE) besides the possible NULL ones. The result of the comparison is 6491 
returned in the boolean Measure bool_var. The original Measure Component of the Data Set op 6492 
is not returned. 6493 
invalid only the invalid (FALSE) Data Points produced by the comparison are returned. The result of 6494 
the comparison (boolean Measure bool_var) is not returned. The original Measure Component 6495 
of the Data Set op is returned and contains the Measure values taken from the Data Points on 6496 
the left side of the rule. 6497 
all_measures all the Data Points produced by the comparison are returned, both the valid ones (TRUE) and 6498 
the invalid ones (FALSE) besides the possible NULL ones. The result of the comparison is 6499 
returned in the boolean Measure bool_var. The original Measure Component of the Data Set op 6500 
is returned and contains the Measure values taken from the Data Points on the left side of the 6501 
rule. 6502 
191 
 
If the parameter output is not specified then it is assumed to be invalid. 6503 
In conclusion, the operator returns a Data Set having the following Components: 6504 
 all the Identifier Components of op 6505 
 the additional Identifier Component ruleid, whose aim is to identify the Rule that has generated the 6506 
actual Data Point (it contains at least the Rule name specified in hr 9) 6507 
 if the output parameter is all: the boolean Measure bool_var whose values are the result of the 6508 
evaluation of the Rules (TRUE, FALSE or NULL). 6509 
 if the output parameter is invalid: the original Measure of op, whose values are taken from the Measure 6510 
values of the Data Points of the left side of the Rule 6511 
 if the output parameter is all_measures: the boolean Measure bool_var, whose value is the result of the 6512 
evaluation of a Rule on a Data Point (TRUE, FALSE or NULL), and the original Measure of op, whose 6513 
values are taken from the Measure values of the Data Points of the left side of the Rule 6514 
 the Measure imbalance, which contains the difference between the Measure values of the Data Points on 6515 
the left side of the Rule and the Measure values of the corresponding calculated Data Points on the right 6516 
side of the Rule 6517 
 the Measure errorcode, which contains the errorcode value specified in the Rule 6518 
 the Measure errorlevel, which contains the errorlevel value specified in the Rule 6519 
 6520 
Note that a gereric Data Point of op can produce several Data Points in the resulting Data Set, one for each Rule 6521 
in which the Data Point appears as the left member of the comparison.  6522 
 6523 
 6524 
Examples 6525 
See also the examples in define hierarchical ruleset. 6526 
 6527 
Given the following hierarchical ruleset: 6528 
 6529 
define hierarchical ruleset  HR_1 ( valuedomain rule  VD_1 )  is 6530 
   R010 : A = J + K + L   errorlevel 5 6531 
;  R020 : B = M + N + O    errorlevel 5 6532 
;  R030 :  C = P + Q  errorcode XX errorlevel 5 6533 
;  R040 : D = R + S    errorlevel 1 6534 
;  R060 : F = Y + W + Z    errorlevel 7 6535 
;  R070 : G = B + C 6536 
;  R080 : H = D + E    errorlevel 0 6537 
;  R090 : I  = D + G  errorcode YY errorlevel 0 6538 
;  R100 : M  >=  N    errorlevel 5 6539 
;  R110 : M  <=  G    errorlevel 5 6540 
end hierarchical ruleset 6541 
 6542 
And given  the operand Data Set DS_1  (where At_1 is viral and the propagation rule says that the alphabetic 6543 
order prevails the NULL prevails on the alphabetic characters and the Attribute value for missing Data Points is 6544 
assumed as NULL): 6545 
 6546 
DS_1 
Id_1 Id_2 Me_1 
2010 A 5 
2010 B 11 
2010 C 0 
2010 G 19 
2010 H NULL 
                                                           
9 The content of ruleid maybe personalised in the implementation 
192 
 
2010 I 14 
2010 M 2 
2010 N 5 
2010 O 4 
2010 P 7 
2010 Q -7 
2010 S 3 
2010 T 9 
2010 U NULL 
2010 V 6 
 6547 
Example 1: DS_r := check_hierarchy ( DS_1, HR_1 rule Id_2 partial_null all ) results in: 6548 
 6549 
DS_r 
Id_1 Id_2 ruleid Bool_var imbalance errorcode errorlevel 
2010 A R010 NULL NULL NULL 5 
2010 B R020 TRUE 0 NULL 5 
2010 C R030 TRUE 0 XX 5 
2010 D R040 NULL NULL NULL 1 
2010 E R050 NULL NULL NULL 0 
2010 F R060 NULL NULL NULL 7 
2010 G R070 FALSE 8 NULL NULL 
2010 H R080 NULL NULL NULL 0 
2010 I R090 NULL NULL YY 0 
2010 M R100 FALSE -3 NULL 5 
2010 M R110 TRUE -17 NULL 5 
 6550 
 6551 
check 6552 
Syntax 6553 
check ( op { errorcode errorcode } { errorlevel errorlevel } { imbalance imbalance } { output } ) 6554 
output ::=  invalid | all 6555 
Input parameters 6556 
op   a boolean Data Set (a boolean condition expressed on one or more Data Sets) 6557 
errorcode  the error code to be produced when the condition evaluates to FALSE. It must be a valid value 6558 
of the errorcode_vd Value Domain (or string if the errorcode_vd Value Domain is not found). 6559 
It can be a Data Set or a scalar. If not specified then errorcode is NULL. 6560 
errorlevel  the error level to be produced when the condition evaluates to FALSE. It must be a valid value 6561 
of the errorlevel_vd Value Domain (or integer if the errorcode_vd Value Domain is not found). 6562 
It can be a Data Set or a scalar. If not specified then errorlevel is NULL. 6563 
193 
 
imbalance  the imbalance to be computed. imbalance is a numeric mono-measure Data Set with the same 6564 
Identifiers of op. If not specified then imbalance is NULL. 6565 
output specifies which Data Points are returned in the resulting Data Set: 6566 
invalid  returns the Data Points of op for which the condition evaluates to 6567 
FALSE 6568 
all  returns all Data Points of op 6569 
If not specified then output is all. 6570 
Examples of valid syntaxes  6571 
check ( DS1 > DS2 errorcode myerrorcode errorlevel myerrorlevel imbalance DS1 - DS2  invalid ) 6572 
Input parameters type: 6573 
op ::  dataset 6574 
errorcode ::  errorcode_vd 6575 
errorlevel ::  errorlevel_vd 6576 
imbalance ::  number 6577 
Result type: 6578 
result ::  dataset 6579 
Additional constraints 6580 
op has exactly a boolean Measure Component. 6581 
Behaviour 6582 
It returns a Data Set having the following components: 6583 
 the Identifier Components of op  6584 
 a boolean Measure named bool_var that contains the result of the evaluation of the boolean dataset op 6585 
 the Measure imbalance that contains the specified imbalance 6586 
 the Measure errorcode that contains the specified errorcode  6587 
 the Measure errorlevel that contains the specified errorlevel 6588 
If output is all then all data points are returned. If output is invalid then only the Data Points where bool_var is 6589 
FALSE are returned. 6590 
 6591 
Examples  6592 
 6593 
Given the Data Sets  DS_1 and  DS_2 : 6594 
 6595 
DS_1 
Id_1 Id_2 Me_1 
2010 I 1 
2011 I 2 
2012 I 10 
2013 I 4 
2014 I 5 
2015 I 6 
2010 D 25 
2011 D 35 
2012 D 45 
194 
 
2013 D 55 
2014 D 50 
2015 D 75 
 6596 
DS_2 
Id_1 Id_2 Me_1 
2010 I 9 
2011 I 2 
2012 I 10 
2013 I 7 
2014 I 5 
2015 I 6 
2010 D 50 
2011 D 35 
2012 D 40 
2013 D 55 
2014 D 65 
2015 D 75 
 6597 
Example 1: DS_r := check ( DS1 >= DS2 imbalance DS1 - DS2 )  returns: 6598 
 6599 
DS_r 
Id_1 Id_2 bool_var imbalance errorcode errorlevel 
2010 I FALSE -8 NULL NULL 
2011 I TRUE 0 NULL NULL 
2012 I TRUE 0 NULL NULL 
2013 I FALSE -3 NULL NULL 
2014 I TRUE 0 NULL NULL 
2015 I TRUE 0 NULL NULL 
2010 D FALSE -25 NULL NULL 
2011 D TRUE 0 NULL NULL 
2012 D TRUE 5 NULL NULL 
2013 D TRUE 0 NULL NULL 
2014 D FALSE  -15 NULL NULL 
2015 D TRUE 0 NULL NULL 
 6600 
195 
 
VTL-ML  -  Conditional operators 6601 
if-then-else :    if 6602 
 6603 
Syntax 6604 
if condition then thenOperand else elseOperand 6605 
 6606 
Input parameters 6607 
 6608 
condition  a Boolean condition (dataset, component or scalar) 6609 
thenOperand  the operand returned when condition evaluates to true  6610 
elseOperand  the operand returned when condition evaluates to false 6611 
 6612 
Examples of valid syntaxes 6613 
if A > B then A else B  6614 
 6615 
Semantics for scalar operations 6616 
The if operator returns thenOperand if condition evaluates to true, elseOperand otherwise. For example, 6617 
considering  the statement:    6618 
if  x1 > x2  then  2  else 5,   6619 
for  x1 = 3,  x2 =0  it returns  2 6620 
for  x1 = 0,  x2 =3  it returns  5 6621 
 6622 
Input Parameters type 6623 
condition :: dataset { measure <boolean> _ }  6624 
|  component<Boolean>  6625 
|  boolean 6626 
thenOperand :: dataset  6627 
|  component  6628 
|  scalar 6629 
elseOperand :: dataset  6630 
|  component  6631 
|  scalar 6632 
 6633 
Result type 6634 
result ::   dataset    6635 
|   component< 6636 
|   scalar 6637 
 6638 
Additional constraints 6639 
 The operands thenOperand and elseOperand must be of the same scalar type. 6640 
 If the operation is at scalar level, thenOperand and elseOperand are scalar then condition must be 6641 
scalar too (a boolean scalar).  6642 
 If the operation is at Component level,  at least one of  thenOperand and elseOperand is a 6643 
Component (the other one can be scalar) and condition must be a Component too (a boolean 6644 
Component); thenOperand,  elseOperand and the other Components referenced in condition must 6645 
belong to the same Data Set.  6646 
 If the operation is at Data Set level,  at least one of  thenOperand and elseOperand is a Data Set (the 6647 
other one can be scalar) and condition must be a Data Set too (having a unique boolean Measure) 6648 
and must have the same Identifiers as thenOperand or/and ElseOperand 6649 
o If thenOperand and elseOperand are both Data Sets then they must have the same 6650 
Components in the same roles  6651 
o If one of thenOperand and elseOperand is a Data Set and the other one is a scalar, the 6652 
Measures of the operand Data Set must be all of the same scalar type as the scalar operand. 6653 
 6654 
 6655 
196 
 
Behaviour 6656 
For operations at Component level, the operation is applied for each Data Point of the unique input Data Set, the 6657 
if-then-else operator returns the value from the thenOperand  Component when  condition evaluates to true,  6658 
otherwise it returns the value from the  elseOperand Component. If one of the operands thenOperand or 6659 
elseOperand is scalar, such a scalar value can be returned depending on the outcome of the condition. 6660 
For operations at Data Set level, the if-then-else operator returns the Data Point from thenOperand  when  the 6661 
Data Point of condition having the same Identifiers’ values evaluates to true,  and returns the Data Point from 6662 
elseOperand otherwise. If one of the operands thenOperand or elseOperand is scalar, such a scalar value can 6663 
be returned (depending on the outcome of the condition) and in this case it feeds the values of all the Measures 6664 
of the result Data Point. 6665 
The behaviour for two Data Sets can be procedurally explained as follows. First the condition Data Set is 6666 
evaluated, then its true  Data Points  are inner joined with thenOperand and its false  Data Points are inner 6667 
joined with elseOperand, finally the union is made of these two partial results (the condition ensures that  there 6668 
cannot be conflicts in the union).  6669 
 6670 
Examples 6671 
 6672 
Example 1:    given the operand Data Sets  DS_cond,  DS_1,  DS_2 : 6673 
 6674 
DS_cond 
Id_1 Id_2 Id_3 Id_4 Me_1 
2012 B Total M 5451780 
2012 B Total F 5643070 
2012 G Total M 5449803 
2012 G Total F 5673231 
2012 S Total M 23099012 
2012 S Total F 23719207 
2012 F Total M 31616281 
2012 F Total F 33671580 
2012 I Total M 28726599 
2012 I Total F 30667608 
2012 A Total M NULL 
2012 A Total F NULL 
 6675 
DS_1 
Id_1 Id_2 Id_3 Id_4 Me_1 
2012 S Total F 25.8 
2012 F Total F NULL 
2012 I Total F 20.9 
2012 A Total M 6.3 
 6676 
DS_2 
Id_1 Id_2 Id_3 Id_4 Me_1 
2012 B Total M 0.12 
2012 G Total M 22.5 
2012 S Total M 23.7 
2012 A Total F NULL 
 6677 
197 
 
DS_r := if ( DS_cond#Id_4 = "F" ) then DS_1 else DS_2   returns: 6678 
 6679 
DS_r 
Id_1 Id_2 Id_3 Id_4 Me_1 
2012 S Total F 25.8 
2012 F Total F NULL 
2012 I Total F 20.9 
Nvl :   nvl 6680 
Syntax 6681 
nvl ( op1 , op2 ) 6682 
 6683 
Input parameters 6684 
op1  the first operand  6685 
op2  the second operand  6686 
 6687 
Examples of valid syntaxes   6688 
nvl ( ds1#m1, 0 ) 6689 
 6690 
Semantics for scalar operations 6691 
The operator nvl returns op2 when op1 is null, otherwise op1. For example: 6692 
nvl ( 5, 0 )  returns   5 6693 
nvl ( null, 0 )  returns   0 6694 
 6695 
Input Parameters type  6696 
op1 ::  dataset    6697 
|   component<scalar> 6698 
|   scalar 6699 
 6700 
op2 ::  dataset  6701 
|   component 6702 
|   <scalar> 6703 
 6704 
Result type 6705 
result ::   dataset   6706 
|   component 6707 
|   scalar 6708 
 6709 
Additional constraints 6710 
If op1 and op2 are scalar values then they must be of the same type. 6711 
If op1 and op2 are Components then they must be of the same type. 6712 
If op1 and op2 are Data Sets then they must have the same Components. 6713 
 6714 
Behaviour 6715 
The operator nvl returns the value from op2 when the value from op1 is null, otherwise it returns the value from  6716 
op1.  6717 
The operator has the typical behaviour of the operators applicable on two scalar values or Data Sets or Data Set 6718 
Components. 6719 
Also the following statement gives the same result:  if isnull ( op1 ) then op2 else op1 6720 
 6721 
Examples 6722 
 6723 
Example 1: Given the input Data Set  DS_1 6724 
 6725 
198 
 
DS_1 
Id_1 Id_2 Id_3 Id_4 Me_1 
2012 B Total Total 11094850 
2012 G Total Total 11123034 
2012 S Total Total NULL 
2012 M Total Total 417546 
2012 F Total Total 5401267 
2012 N Total Total NULL 
 6726 
DS_r   := nvl ( DS_1, 0 )   returns: 6727 
 6728 
DS_r 
Id_1 Id_2 Id_3 Id_4 Me_1 
2012 B Total Total 11094850 
2012 G Total Total 11123034 
2012 S Total Total 0 
2012 M Total Total 417546 
2012 F Total Total 5401267 
2012 N Total Total 0 
199 
 
VTL-ML  -  Clause operators 6729 
Filtering Data Points :  filter 6730 
 6731 
Syntax   6732 
op  [ filter  filterCondition ] 6733 
 6734 
Input parameters 6735 
op    the  operand  6736 
filterCondition   the  filter  condition  6737 
 6738 
Examples of valid syntaxes  6739 
DS_1 [ filter Me_3 > 0 ] 6740 
DS_1 [ filter  Me_3 + Me_2 <= 0 ] 6741 
 6742 
Semantics for scalar operations 6743 
This operator cannot be applied to scalar values.  6744 
 6745 
Input parameters type: 6746 
op ::    dataset  6747 
filterCondition ::   component<boolean> 6748 
 6749 
Result type: 6750 
result ::   dataset 6751 
 6752 
Additional constraints: 6753 
None. 6754 
 6755 
Behaviour 6756 
The operator takes as input a Data Set (op) and a boolean Component expression (filterCondition) and filters the 6757 
input Data Points according to the evaluation of the condition. When the expression is TRUE the Data Point is 6758 
kept in the result, otherwise it is not kept (in other words, it filters out the Data Points of the operand Data Set 6759 
for which filterCondition condition evaluates to FALSE or NULL). 6760 
 6761 
Examples 6762 
 6763 
Given the Data Set DS_1: 6764 
DS_1 
Id_1 Id_2 Id_3 Me_1 At_1 
1 A XX 2 E 
1 A YY 2 F 
1 B XX 20 F 
1 B YY 1 F 
2 A XX 4 E 
2 A YY 9 F 
 6765 
Example1:  DS_r := DS_1  [ filter Id_1 = 1 and Me_1 < 10 ]  results in: 6766 
 6767 
DS_r 
Id_1 Id_2 Id_3 Me_1 At_1 
200 
 
1 A XX 2 E 
1 A YY 2 F 
1 B YY 1 F 
Calculation of a Component :  calc 6768 
 6769 
Syntax   6770 
op [ calc { calcRole } calcComp := calcExpr { , { calcRole } calcComp := calcExpr }* ] 6771 
 6772 
 calcRole ::=  identifier  |  measure  |  attribute  |  viral attribute 6773 
 6774 
Input parameters 6775 
op   the operand 6776 
calcRole the role to ba assigned to a Component to  be calculated 6777 
calcComp the name of a Component to be calculated 6778 
calcExpr  expression at component level, having only Components of the input Data Sets as operands, 6779 
used to calculate a Component 6780 
 6781 
Examples of valid syntaxes  6782 
DS_1 [ calc Me_3 := Me_1 + Me_2 ] 6783 
 6784 
Semantics for scalar operations 6785 
This operator cannot be applied to scalar values.  6786 
 6787 
Input parameters type: 6788 
op ::   dataset 6789 
calcComp :: name < component > 6790 
calcExpr ::  component<scalar> 6791 
 6792 
Result type: 6793 
result ::  dataset 6794 
 6795 
Additional constraints 6796 
The calcComp parameter cannot be the name of an Identifier component.  6797 
All the components used in calcComp must belong to the operand Data Set op. 6798 
 6799 
Behaviour 6800 
The operator calculates new Identifier, Measure or Attribute Components on the basis of sub-expressions at 6801 
Component level. Each Component is calculated through an independent sub-expression.  It is possible to specify 6802 
the role of the calculated Component among measure, identifier, attribute, or viral attribute, therefore the calc 6803 
clause can be used also to change the role of a Component when possible. The keyword viral allows controlling 6804 
the virality of the calculated Attributes (for the attribute propagation rule see the User Manual). When the role is 6805 
omitted, the following rule is applied: if the component exists in the operand Data Set then it maintains its role; if 6806 
the component does not exist in the operand Data Set then its role is Measure.  6807 
The calcExpr sub-expressions are independent one another, they can only reference Components of the input 6808 
Data Set and cannot use Components generated, for example, by other calcExpr. If the calculated Component is a 6809 
new Component, it is added to the output Data Set. If the Calculated component is a Measure or an Attribute that 6810 
already exists in the input Data Set, the calculated values overwrite the original values. If the calculated 6811 
Component is an Identifier that already exists in the input Data Set, an exception is raised because overwriting 6812 
an Identifier Component is forbidden for preserving the functional behaviour. Analytic invocations can be used 6813 
in the calc clause. 6814 
 6815 
 6816 
Examples 6817 
 6818 
 6819 
Given the Data Set DS_1: 6820 
201 
 
DS_1 
Id_1 Id_2 Id_3 Me_1 
1 A CA 20 
1 B CA 2 
2 A CA 2 
 6821 
Example1:  DS_r := DS_1 [ calc Me_1:= Me_1 * 2 ]   results in: 6822 
 6823 
DS_r 
Id_1 Id_2 Id_3 Me_1 
1 A CA 40 
1 B CA 4 
2 A CA 4 
 6824 
Example2:  DS_r := DS_1 [ calc attribute At_1:= “EP” ]   results in: 6825 
 6826 
DS_r 
Id_1 Id_2 Id_3 Me_1 At_1 
1 A CA 40 EP 
1 B CA 4 EP 
2 A CA 4 EP 
 6827 
Aggregation :  aggr 6828 
 6829 
Syntax   6830 
op [ aggr aggrClause { groupingClause } ]  6831 
 6832 
aggrClause ::= { aggrRole } aggrComp := aggrExpr  6833 
{ , { aggrRrole } aggrComp:= aggrExpr }*  6834 
 6835 
groupingClause ::= { group by   groupingId {, gropuingId }*  6836 
| group except groupingId {, groupingId }*  6837 
| group all conversionExpr }1 6838 
  { having havingCondition }   6839 
 6840 
aggrRole::=  measure  |  attribute  |  viral attribute 6841 
 6842 
 6843 
Input Parameters 6844 
op the operand  6845 
aggrClause clause that specifies the required aggregations, i.e., the aggregated Components to be 6846 
calculated, their roles and their calculation algorithm, to be applied on the joined and 6847 
filtered Data Points 6848 
aggrRole the role of the aggregated Component to be calculated 6849 
aggrComp the name of the aggregated Component to be calculated; this is a dependent Component 6850 
of the result (Measure or Attribute, not Identifier) 6851 
202 
 
aggrExpr expression at component level, having only Components of the input Data Sets as 6852 
operands, which invokes an aggregate operator (e.g.  avg, count, max … , see also the 6853 
corresponding sections) to perform the desired aggregation. Note that the count 6854 
operator is used in an aggrClause without parameters, e.g.:  6855 
DS_1 [ aggr Me_1 := count ( ) group by Id_1 ) ] 6856 
groupingClause the following alternative grouping options: 6857 
group by the Data Points are grouped by the values of the specified Identifiers 6858 
(groupingId). The Identifiers not specified are dropped in the result. 6859 
group except the Data Points are grouped by the values of the Identifiers not 6860 
specified as groupingId. The Identifiers specified as groupingId are 6861 
dropped in the result. 6862 
group all converts the values of an Identifier Component using conversionExpr 6863 
and keeps all the resulting Identifiers. 6864 
groupingId Identifier Component to be kept (in the group by clause) or dropped (in the group 6865 
except clause). 6866 
conversionExpr specifies a conversion operator (e.g., time_agg) to convert an Identifier from finer to 6867 
coarser granularity. The conversion operator is applied on an Identifier of the operand 6868 
Data Set op. 6869 
havingCondition a condition (boolean expression) at component level, having only Components of the 6870 
input Data Sets as operands (and possibly constants), to be fulfilled by the groups of 6871 
Data Points:  only groups for which havingCondition evaluates to TRUE appear in the 6872 
result. The havingCondition refers to the groups specified through the groupingClause, 6873 
therefore it must invoke aggregate operators (e.g.  avg, count, max …, see also the 6874 
section Aggregate invocation). A correct example of havingCondition is:   6875 
max(obs_value) < 1000  6876 
instead the condition obs_value < 1000 is not a right havingCondition, because it 6877 
refers to the values of the single Data Points and not to the groups. The count operator 6878 
is used in a havingCondition without parameters, e.g.:  6879 
sum (DS_1 group by id1 having count ( ) >= 10 ) 6880 
 6881 
Examples of valid syntaxes 6882 
DS_1 [ aggr M1 := min ( Me_1 ) group by  Id_1, Id_2  ] 6883 
DS_1 [ aggr M1 := min ( Me_1 ) group except  Id_1, Id_2 ] 6884 
 6885 
Semantics for scalar operations 6886 
This operator cannot be applied to scalar values.  6887 
 6888 
Input parameters type: 6889 
op ::    dataset 6890 
aggrComp ::   name < component > 6891 
aggrExpr ::   component<scalar> 6892 
groupingId ::  name <identifier > 6893 
conversionExpr ::  identifier<scalar> 6894 
havingCondition :: component<boolean> 6895 
 6896 
Result type: 6897 
result ::  dataset 6898 
 6899 
Additional constraints 6900 
The aggrComp parameter cannot be the name of an Identifier component.  6901 
All the components used in aggrExpr must belong to the operand Data Set op. 6902 
The conversionExpr parameter applies just one conversion operator to just one Identifier belonging to the input 6903 
Data Set. The basic scalar type of the Identifier must be compatible with the basic scalar type of the conversion 6904 
operator.  6905 
 6906 
203 
 
Behaviour 6907 
The operator aggr calculates aggregations of dependent Components (Measures or Attributes) on the basis of  6908 
sub-expressions at Component level. Each Component is calculated through an independent sub-expression.  It is 6909 
possible to specify the role of the calculated Component among measure attribute, or viral attribute. The 6910 
substring viral allows to control the virality of Attributes, if the Attribute propagation rule is adopted (see the 6911 
User Manual). When the role is omitted, the following rule is applied: if the component exists in the operand Data 6912 
Set then it maintains its role; if the component does not exist in the operand Data Set then its role is Measure.  6913 
The aggrExpr sub-expressions are independent of one another, they can only reference Components of the input 6914 
Data Set and cannot use Components generated, for example, by other aggrExpr sub-expressions. The aggr 6915 
computed Measures and Attributes are the only Measures and Attributes returned in the output Data Set (plus 6916 
the possible viral Attributes). The sub-expressions must contain only Aggregate operators, which are able to 6917 
compute an aggregated Value relevant to a group of Data Points. The groups of Data Points to be aggregated are 6918 
specified through the groupingClause, which allows the following alternative options. 6919 
group by the Data Points are grouped by the values of the specified Identifiers. The Identifiers not 6920 
specified are dropped in the result. 6921 
group except the Data Points are grouped by the values of the Identifiers not specified in the clause. The 6922 
specified Identifiers are dropped in the result. 6923 
group all converts an Identifier Component using conversionExpr and keeps all the other Identifiers. 6924 
 6925 
The having clause is used to filter groups in the result by means of an aggregate condition evaluated on the 6926 
single groups (for example the minimum number of Data Points in the group).  6927 
If no grouping clause is specified, then all the input Data Points are aggregated in a single group and the clause 6928 
returns a Data Set that contains a single Data Point and has no Identifiers. 6929 
The Attributes calculated through the aggr clauses are maintained in the result. For all the other Attributes that 6930 
are defined as viral, the Attribute propagation rule is applied (for the semantics, see the Attribute Propagation 6931 
Rule section in the User Manual). 6932 
 6933 
 6934 
Examples 6935 
 6936 
Given the Data Set DS_1: 6937 
DS_1 
Id_1 Id_2 Id_3 Me_1 
1 A XX 0 
1 A YY 2 
1 B XX 3 
1 B YY 5 
2 A XX 7 
2 A YY 2 
 6938 
Example1:  DS_r := DS_1 [ aggr Me_1:= sum( Me_1 ) group by Id_1 , Id_2 ]  results in: 6939 
 6940 
DS_r 
Id_1 Id_2 Me_1 
1 A 2 
1 B 8 
2 A 9 
 6941 
Example2:  DS_r := DS_1 [ aggr Me_3:= min( Me_1 ) group except  Id_3 ]  results in: 6942 
 6943 
204 
 
DS_r 
Id_1 Id_2 Me_3 
1 A 0 
1 B 3 
2 A 2 
 6944 
Example3:  DS_r := DS_1 [ aggr Me_1:= sum( Me_1 ), Me_2 := max( Me_1)   6945 
 group by Id_1 , Id_2  6946 
having mean (Me_1 ) > 2  ]   results in: 6947 
 6948 
 6949 
DS_r 
Id_1 Id_2 Me_1 Me_2 
1 B 8 5 
2 A 9 7 
 6950 
Maintaining Components:  keep 6951 
 6952 
Syntax   6953 
op [ keep comp {, comp }* ] 6954 
 6955 
Input parameters 6956 
op  the operand  6957 
comp   a component to keep 6958 
 6959 
Examples of valid syntaxes  6960 
DS_1 [ keep Me_2, Me_3 ] 6961 
 6962 
Semantics for scalar operations 6963 
This operator cannot be applied to scalar values.  6964 
 6965 
Input parameters type: 6966 
op ::  dataset 6967 
comp ::   name < component > 6968 
 6969 
Result type: 6970 
result ::  dataset 6971 
 6972 
Additional constraints: 6973 
All the Components comp must belong to the input Data Set op. 6974 
The Components comp cannot be Identifiers in op. 6975 
 6976 
Behaviour 6977 
The operator takes as input a Data Set (op) and some Component names of such a Data Set (comp). These 6978 
Components can be Measures or Attributes of op but not Identifiers. The operator maintains the specified 6979 
Components, drops all the other dependent Components of the Data Set (Measures and Attributes) and 6980 
maintains the independent Components (Identifiers) unchanged. This operation corresponds to a projection in 6981 
the usual relational join semantics (specifying which columns will be projected in among Measures and 6982 
Attributes).  6983 
 6984 
 6985 
205 
 
Examples 6986 
 6987 
Given the Data Set DS_1: 6988 
DS_1 
Id_1 Id_2 Id_3 Me_1 Me_2 At_1 
2010 A XX 20 36 E 
2010 A YY 4 9 F 
2010 B XX 9 10 F 
 6989 
Example1:  DS_r := DS_1 [ keep  Me_1  ]  results in: 6990 
 6991 
DS_r 
Id_1 Id_2 Id_3 Me_1 
2010 A XX 20 
2010 A YY 4 
2010 B XX 9 
 6992 
Removal of Components: drop 6993 
 6994 
Syntax   6995 
op [drop  comp { , comp }* ] 6996 
 6997 
Input parameters 6998 
op   the operand 6999 
comp   a Component to drop 7000 
 7001 
Examples of valid syntaxes  7002 
DS_1 [ drop  Me_2, Me_3 ] 7003 
 7004 
Semantics for scalar operations 7005 
This operator cannot be applied to scalar values.  7006 
 7007 
Input parameters type: 7008 
op ::   dataset  7009 
comp ::   name < component > 7010 
 7011 
Result type: 7012 
result ::  dataset 7013 
 7014 
Additional constraints: 7015 
All the Components comp must belong to the input Data Set op. 7016 
The Components comp cannot be Identifiers in op. 7017 
 7018 
Behaviour 7019 
The operator takes as input a Data Set (op) and  some Component names of such a Data Set (comp). These 7020 
Components can be Measures or Attributes of op but not Identifiers. The operator drops the specified 7021 
Components and  maintains all the other Components of the Data Set. This operation corresponds to a projection 7022 
in the usual relational join semantics (specifying which columns will be projected out).  7023 
 7024 
Examples 7025 
 7026 
206 
 
Given the Data Set DS_1: 7027 
 7028 
DS_1 
Id_1 Id_2 Id_3 Me_1 At_1 
2010 A XX 20 E 
2010 A YY 4 F 
2010 B XX 9 F 
 7029 
Example1:  DS_r := DS_1 [ drop  At_1 ]   results in: 7030 
 7031 
DS_r 
Id_1 Id_2 Id_3 Me_1 
2010 A XX 20 
2010 A YY 4 
2010 B XX 9 
Change of Component name :  rename 7032 
Syntax   7033 
op [ rename  comp_from  to  comp_to  { , comp_from  to  comp_to}*  ] 7034 
 7035 
Input Parameters 7036 
op    the operand  7037 
comp_from   the original name of the Component to rename 7038 
comp_to   the new name of the Component after the renaming 7039 
 7040 
Examples of valid syntaxes  7041 
DS_1 [ rename Me_2 to Me_3 ] 7042 
 7043 
Semantics for scalar operations 7044 
This operator cannot be applied to scalar values.  7045 
 7046 
Input Parameters type  7047 
op ::       dataset   7048 
comp_from ::    name < component > 7049 
comp_to ::   name < component > 7050 
 7051 
Result type 7052 
result ::        dataset 7053 
 7054 
Additional constraints 7055 
The corresponding pairs of Components before and after the renaming (dsc_from and dsc_to) must be defined 7056 
on the same Value Domain and the same Value Domain Subset.  7057 
The components used in dsc_from must belong to the input Data Set and the component used in the dsc_to 7058 
cannot have the same names as other Components of the result Data Set. 7059 
 7060 
Behaviour  7061 
The operator assigns new names to one or more Components (Identifier, Measure or Attribute Components). 7062 
The resulting Data Set, after renaming the specified Components, must have unique names of all its Components 7063 
(otherwise a runtime error is raised). Only the Component name is changed and not the Component Values, 7064 
therefore the new Component must be defined on the same Value Domain and Value Domain Subset as the 7065 
original Component (see also the IM in the User Manual). If the name of a Component defined on a different 7066 
207 
 
Value Domain or Set is assigned, an error is raised. In other words, rename is a transformation of the variable 7067 
without any change in its values.  7068 
 7069 
 7070 
Examples 7071 
 7072 
Given the Data Set DS_1: 7073 
 7074 
DS_1 
Id_1 Id_2 Id_3 Me_1 At_1 
1 B XX 20 F 
1 B YY 1 F 
2 A XX 4 E 
2 A YY 9 F 
 7075 
Example1: DS_r := DS_1  [ rename  Me_1 to Me_2, At_1 to At_2] results in: 7076 
 7077 
DS_r 
Id_1 Id_2 Id_3 Me_2 At_2 
1 B XX 20 F 
1 B YY 1 F 
2 A XX 4 E 
2 A YY 9 F 
Pivoting :  pivot 7078 
 7079 
Syntax   7080 
op [ pivot identifier , measure ] 7081 
 7082 
Input parameters 7083 
op    the operand 7084 
identifier  the Identifier Component of op to pivot 7085 
measure  the Measure Component of op to pivot 7086 
 7087 
 7088 
Examples of valid syntaxes  7089 
DS_1 [ pivot  Id_2,  Me_1 ] 7090 
 7091 
Semantics for scalar operations 7092 
This operator cannot be applied to scalar values.  7093 
 7094 
Input Parameters type  7095 
op ::   dataset 7096 
identifier ::  name < identifier > 7097 
measure ::  name < measure > 7098 
 7099 
Result type 7100 
result ::        dataset 7101 
 7102 
208 
 
Additional constraints 7103 
The Measures created by the operator according to the behaviour described below must be defined on the same  7104 
Value Domain as the input Measure. 7105 
 7106 
Behaviour  7107 
The operator transposes several Data Points of the operand Data Set into a single Data Point of the resulting Data 7108 
Set. The semantics of pivot can be procedurally described as follows. 7109 
 7110 
1. It creates a virtual Data Set VDS as a copy of op 7111 
2. It drops the Identifier Component identifier and all the Measure Components from VDS. 7112 
3. It groups VDS by the values of the remaining Identifiers. 7113 
4. For each distinct value of identifier in op, it adds a corresponding measure to VDS, named as the value of 7114 
identifier. These Measures are initialized with the NULL value. 7115 
5. For each Data Point of op, it finds the Data Point of VDS having the same values as for the common 7116 
Identifiers and assigns the value of measure (taken from the current Data Point of op) to the Measure of 7117 
VDS having the same name as the value of identifier (taken from the Data Point of op). 7118 
 7119 
The result of the last step is the output of the operation. 7120 
 7121 
Note that pivot may create Measures whose names are non-regular (i.e. they may contain special characters, 7122 
reserved keywords, etc.) according to the rules about the artefact names described in the User Manual (see the 7123 
section “The artefact names” in the chapter “VTL Transformations”).  As said in the User Manual, those names 7124 
must be quoted to be referenced within an expression. 7125 
 7126 
Examples 7127 
 7128 
Given the Data Set DS_1: 7129 
 7130 
DS_1 
Id_1 Id_2 Me_1 At_1 
1 A 5 E 
1 B 2 F 
1 C 7 F 
2 A 3 E 
2 B 4 E 
2 C 9 F 
 7131 
Example1: DS_r := Ds_1 [ pivot  Id_2,  Me_1 ]   results in: 7132 
 7133 
DS_r 
Id_1 A B C 
1 5 2 7 
2 3 4 9 
 7134 
Unpivoting : unpivot 7135 
 7136 
Syntax   7137 
op [ unpivot  identifier , measure ] 7138 
 7139 
209 
 
Input parameters 7140 
op    the dataset operand 7141 
identifier  the Identifier Component to be created 7142 
measure   the Measure Component to be created 7143 
 7144 
Examples of valid syntaxes  7145 
DS [ unpivot   Id_5,  Me_3 ] 7146 
 7147 
Semantics for scalar operations 7148 
This operator cannot be applied to scalar values.  7149 
 7150 
Input Parameters type  7151 
op ::   dataset  7152 
identifier ::  name < identifier > 7153 
measure ::   name < measure > 7154 
 7155 
Result type 7156 
result ::        dataset 7157 
 7158 
Additional constraints 7159 
All the measures of op must be defined on the same Value Domain. 7160 
 7161 
Behaviour  7162 
The unpivot operator transposes a single Data Point of the operand Data Set into several Data Points of the 7163 
result Data set. Its semantics can be procedurally described as follows.  7164 
 7165 
1. It creates a virtual Data Set VDS as a copy of op 7166 
2. It adds adds the Identifier Component identifier and the Measure Component measure to VDS. 7167 
3. For each Data Point DP and for each Measure M of op whose value is not NULL, the operator inserts a 7168 
Data Point into VDS whose values are assigned as specified in the following points 7169 
4. The VDS Identifiers other than identifier are assigned the same values as the corresponding Identifiers of 7170 
the op Data Point 7171 
5. The VDS identifier is assigned a value equal to the name of the Measure M of op  7172 
6. The VDS measure is assigned a value equal to the value of the Measure M of op  7173 
 7174 
The result of the last step is the output of the operation. 7175 
 7176 
When a Measure is NULL then unpivot does not create a Data Point for that Measure. 7177 
Note that in general pivoting and unpivoting are not exactly symmetric operations, i.e., in some cases the unpivot 7178 
operation applied to the pivoted Data Set does not recreate exactly the original Data Set (before pivoting). 7179 
 7180 
Examples 7181 
 7182 
Given the Data Set DS_1: 7183 
 7184 
DS_1 
Id_1 A B C 
1 5 2 7 
2 3 4 9 
 7185 
 7186 
Example1: DS_r := DS_1 [ unpivot Id_2, Me_1]   results in: 7187 
 7188 
DS_r 
Id_1 Id_2 Me_1 
210 
 
1 A 5 
1 B 2 
1 C 7 
2 A 3 
2 B 4 
2 C 9 
 7189 
Subspace : sub 7190 
 7191 
Syntax   7192 
op [ sub identifier = value { , identifier = value }* ] 7193 
 7194 
Input parameters 7195 
op    dataset 7196 
identifier Identifier Component of the input Data Set op 7197 
value   valid value for identifier  7198 
 7199 
Examples of valid syntaxes  7200 
DS_r := DS_1 [ Id_2 = "A", Id_5 = 1 ] 7201 
 7202 
Semantics for scalar operations 7203 
This operator cannot be applied to scalar values.  7204 
 7205 
Input Parameters type  7206 
op ::   dataset 7207 
identifier :: name < identifier > 7208 
value ::   scalar 7209 
 7210 
Result type 7211 
result ::   dataset 7212 
 7213 
Additional constraints 7214 
The specified Identifier Components identifier(s) must belong to the input Data Set op.  7215 
Each Identifier Component can be specified only once.  7216 
The specified value must be an allowed value for identifier. 7217 
 7218 
 7219 
Behaviour  7220 
 7221 
The operator returns a Data Set in a subspace of the one of the input Dataset. Its behaviour can be procedurally 7222 
described as follows: 7223 
 7224 
1. It creates a virtual Data Set VDS as a copy of op 7225 
2. It maintains the Data Points of VDS for which identifier = value (for all the specified identifier) and 7226 
eliminates  all the Data Points for which  identifier <> value  (even for only one specified identifier) 7227 
3. It projects out (“drops”, in VTL terms) all the identifier(s)  7228 
 7229 
The result of the last step is the output of the operation. 7230 
 7231 
The resulting Data Set has the Identifier Components that are not specified as identifier(s) and has the same 7232 
Measure and Attribute Components of the input Data Set.   7233 
 7234 
The result Data Set does not violate the functional constraint because after the filter of the step 2, all the 7235 
remaining identifier(s) do not contain the same Values for all the Data Points. In other words, given that the input 7236 
211 
 
Data Set is a 1st order function and therefore does not contain duplicates, the result Data Set is a 1st order 7237 
function as well. To show this, let K1,…,Km,…,Kn be the Identifier components for the generic input Data Set DS. 7238 
Let us suppose that K1,…,Km are assigned to fixed values by using the subspace operator. A duplicate could arise 7239 
only if in the result there are two Data Points DPr1 and DPr2 having the same value for Km+1,…,Kn , but this is 7240 
impossible since such Data Points had same K1,…,Km in the original Data Set DS, which did not contain 7241 
duplicates. 7242 
 7243 
If we consider the vector space of Data Points individuated by the n-uples of Identifier components of a Data Set 7244 
DS(K1,…,Kn,…) (along, e.g., with the operators of sum and multiplication), we have that the subspace operator 7245 
actually performs a subsetting of such space into another space with fewer Identifiers. This can be also seen as 7246 
the equivalent of a dice operation performed on hyper-cubes in multi-dimensional data warehousing. 7247 
 7248 
 7249 
Examples 7250 
 7251 
Given the Data Set DS_1:  7252 
 7253 
DS_1 
Id_1 Id_2 Id_3 Me_1 At_1 
1 A XX 20 F 
1 A YY 1 F 
1 B XX 4 E 
1 B YY 9 F 
2 A XX 7 F 
2 A YY 5 E 
2 B XX 12 F 
2 B YY 15 F 
 7254 
Example1:  DS_r := DS_1 [ sub  Id_1 = 1,  Id_2 = “A” ]   results in: 7255 
 7256 
DS_r 
Id_3 Me_1 At_1 
XX 20 F 
YY 1 F 
 7257 
Example 2:  DS_r := DS_1 [ sub Id_1 =  1, Id_2 = “B”, Id_3 = “YY” ]  results in: 7258 
 7259 
DS_r 
Me_1 At_1 
9 F 
 7260 
Example 3:  DS_r :=  DS_1 [ sub  Id_2 = “A” ] +  DS_1 [ sub Id_2 = “B” ]  results in: 7261 
  7262 
 7263 
Assuming that At_1 is viral and that in the propagation rule the greater value prevails, results in: 7264 
 7265 
DS_r 
Id_1 Id_3 Me_1 At_1 
1 XX 24 F 
212 
 
1 YY 10 F 
2 XX 19 F 
2 YY 20 F 
 7266 
 7267 
 7268 
