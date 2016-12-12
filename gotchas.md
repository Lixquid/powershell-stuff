<h1 align="center">Powershell Gotchas</h1>

[↖︎ Back to Index](index.html)

1. Single element arrays act like the single element.

   ``` powershell
   > [bool]( @(5) -eq 5 )
   True
   ```

2. `$null` responds to all methods.

   ``` powershell
   > $null.invalid_method
   # *No Error*
   ```

3. `$null` responds to `Count`.
   
   ``` powershell
   > $null.Count
   0
   ```

4. Functions are called with spaces.

   ``` powershell
   > Test 1 2 3
   ```

5. Functions will fail silently when called with parenthesis and commas.

   ``` powershell
   > Test( 1, 2, 3 )
   # *Calls Test with a single argument; an array containing 1, 2, 3*
   ```

6. Don't use $input as a variable name.

   ``` powershell
   > $input = 5
   > $input
   # *No Output*
   ```

7. By Default, Powershell errors do not halt execution.

   ``` powershell
   > asdf; echo 5
   # *ERROR*
   5
   ```

8. `param` in a script will error if given parameters that have default values
   **if** there are statements before the param block.
   
   ``` powershell
   > echo 5; param( $a, $b )
   # *Ok*
   > echo 5; param( $a = 5, $b )
   # *ERROR*
   ```

9. Just don't use workflows.
10. Do not rethrow an exception explicitly in a `catch` block, use a bare
    `throw`.
    
    ``` powershell
    > try { invalid_method } `
    . catch { throw $_.Exception }
    # *ERROR: Line 2*
    > try { invalid_method } `
    . catch { throw }
    # *ERROR: Line 1*
    ```

<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-alpha.5/css/bootstrap.min.css" integrity="sha384-AysaV+vQoT3kOAXZkl02PThvDr8HYKPZhNT5h/CXfBThSRXQ6jW5DO2ekP5ViFdi" crossorigin="anonymous">
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-alpha.5/js/bootstrap.min.js" integrity="sha384-BLiI7JTZm+JWlgKa0M0kGRpJbF2J8q+qreVrKBC47e3K6BW78kGLrCkeRX6I9RoK" crossorigin="anonymous"></script>
