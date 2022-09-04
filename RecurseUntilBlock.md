#SmartBlock RecurseUntil
  <%NOBLOCKOUTPUT%>Documentation
     ^^After downloading I recommend putting <%HIDE%> in the name of the smartblock^^
     ^^Please note that this block is meant to be used with other blocks as an intermediate. It expects certain variables to have contents to be able to run.^^
     ^^Please note that if you need to run a for loop (simple iteration) you can use a nested smartblock and repeat call^^
        <%REPEAT,number of times,<%SMARTBLOCK:Block to call%>%>
     This block takes several arguments and then runs until a test has been completed.
        Please set the variable **recurse_until_var_name** to the variable name you want to check
        Please set the variable **recurse_until_test** to the value you wish to test against
        Please set the variable **recurse_until_callee** to the name of the block you would like called
        Please set the variable **recurse_until_max_iterations** to the maximum number of times
        you would like to run this loop before it forces itself to break. Set this to -1 to force the 
        block to ignore it. ^^**DO NOT SET THIS TO ANY NEGATIVE VALUES OTHER THAN -1**^^
            This argument is mainly meant for testing purposes
            In practice when building a complex block you should make sure your iterations each tend towards some final state otherwise you will lock up RoamResearch entirely
        The following is a brief example of how you could do this in a block
          HashtagSmartBlock Looper
             <%SET:recurse_until_var_name,joseph_gordon_levitt%>
             <%SET:recurse_until_test_value,bruce willis%> 
             <%SET:recurse_until_callee,Continue movie%>
             <%SET:recurse_until_max_iterations,-1%>
             <%NOBLOCKOUTPUT%>
             <%SMARTBLOCK: RecurseUntil%>
    - <%NOBLOCKOUTPUT%>#[[Smartblock Comment]] ^^Checking on the max iterations. If equal exit^^
    - <%IFVAR:recurse_until_max_iterations,/(?:-1|0)/%><%EXIT%><%NOBLOCKOUTPUT%>
    - <%NOBLOCKOUTPUT%>#[[Smartblock Comment]] ^^Checking on the test value if equal, exit^^
    - <%IFVAR:<%GET:recurse_until_var_name%>,<%GET:recurse_until_test_value%>%><%EXIT%><%NOBLOCKOUTPUT%>
    - <%NOBLOCKOUTPUT%>#[[Smartblock Comment]] ^^If the value of max iterations is not equal to one, decrement it^^
    - <%IFNOTVAR:recurse_until_max_iterations,-1%><%SET:recurse_until_max_iterations,<%DIFFERENCE:<%GET:recurse_until_max_iterations%>,1%>%>
    - <%SMARTBLOCK:<%GET:recurse_until_callee%>%><%SMARTBLOCK:RecurseUntil%>
