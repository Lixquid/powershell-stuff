<h1 align="center">Powershell Tricks</h1>

[↖︎ Back to Index](index.html)

1. You can promote a block of commands to halting errors by wrapping them in a
   `try` block with an empty `finally` block.
   
   ``` powershell
   > foo; bar
   # *ERROR: foo not recognized*
   # *ERROR: bar not recognized*
   > try { foo; bar } finally {}
   # *ERROR: foo not recognized*
   ```

2. You can redirect any output stream (Error, Verbose, Debug) into standard
   standard input (the stream the input pipe uses).
   
   ``` powershell
   > Write-Error hello | Write-Host
   # *ERROR: hello*
   > Write-Error hello 2>&1 | Write-Host
   hello
   ```
   
   - **1**: Standard Output
   - **2**: Error
   - **3**: Warning
   - **4**: Verbose
   - **5**: Debug

3. You can find the fully qualified class name of an exception by using
   `select -Property *`

   ``` powershell
   > try { 0/0 } catch { $_ | select -Property * }
   ...
   Exception: System.Management.Automation.RuntimeException ...
   ...
   ```

4. You can pass a Hash or Array of objects into a commandlet to use them as
   Named parameters or Positional Parameters respectively.
   
   ``` powershell
   > function x( $a, $b, $c ) { echo "A: $a | B: $b | C: $c" }
   > $i = @( 1, 2, 3 )
   > x @i
   A: 1 | B: 2 | C: 3
   > $i = @{ a = 4; b = 5; c = 6 }
   > x @i
   A: 4 | B: 5 | C: 6
   ```
