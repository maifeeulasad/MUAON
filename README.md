# MUAON

MUAON is an OBJECT notation introduced by Maifee Ul Asad, it has some similarities with JSON. But it takes less space than JSON. Although it is easily readable like JSON.

## Motivation behind devloping MUAON

Share extensive ammount of simmilar data.


## Grammar
```
MUAON 				: '{' DEF_BLOCK DATA_BLOCK '}';

DEF_BLOCK 			: 'def' '=' '[' ']'
         			| 'def' '=' '[' DEF_SET ']';

DEF_SET 			: DEF
              		        | DEF_SET ',' DEF;

DEF     			: integer '(' ')'
                	        | integer '(' KEY_SET ')';

KEY 				: KEYELEM+;

KEY_SET 			: KEY
       				| integer
       				| KEY_SET ',' KEY
       				| KEY_SET ',' integer;

DATA_BLOCK 			: 'data' '=' VALUE;

VALUE 				: STRING 
				| OBJECT 
				| ARRAY 
				| bool
				| integer 
				| float;

bool 				: 'true' | 'false';

OBJECT 				: '{' '}'
        			| '{' ',' VALUE_SET_OBJECT '}'
        			| '{' integer ',' VALUE_SET_OBJECT '}';

VALUE_SET_OBJECT    		: VALUE
                		| VALUE_SET_OBJECT ',' VALUE
                		| VALUE_SET_OBJECT ',';

ARRAY 				: '[' ']'
      				| '[' integer ',' VALUE_SET_ARRAY ']'
     				| '[' '$' ',' VALUE_SET_ARRAY ']';

VALUE_SET_ARRAY 		: VALUE
            			| VALUE_SET_ARRAY ',' VALUE;



integer 			: '-'? DIGIT+;

float 				: '-' ? integer ( ('.' DIGIT+ EXPONENT?) | (EXPONENT));
EXPONENT 			: [eE] [-+]? integer+;
DIGIT 				: '0'..'9';



KEYELEM 			: [0-9a-zA-Z];

STRING 				: '"' (~["\\] | ESCAPE)* '"';
ESCAPE 				: '\\' ( ["\\/bfnrt]| UNICODE) ;
UNICODE 			: 'u' HEXADECIMAL HEXADECIMAL HEXADECIMAL HEXADECIMAL;
HEXADECIMAL			: [0-9a-fA-F];

WHITE_SPACE 			: [\r\n\t ]+ -> skip;
MULTI_COMMENTS 			: '/*' .*? '*/' -> skip;

```

## So whats the difference ?

Let's keep this really short and on point. Want to pass data of same type like students ? In JSON, what would we do, we pass an ARRAY of students, where each and every OBJECT consists of KEY-VALUE pair. Is it necessay ? No. First just send those OBJECT DEFs, means what are the shape of those OBJECTs, then you can say this is the ARRAY of student type, here comes the data. I think now the grammar is more readable.

WIP - doc


## Tanslator
 - MUAON to JSON
   - Antlr : https://github.com/maifeeulasad/MUAON2JSON
