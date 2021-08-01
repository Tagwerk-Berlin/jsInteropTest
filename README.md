# jsInteropTest
Blazor Interop

*Pass all keystrokes to .NET*

Blazor example for JS Interop.
.Net call in javascript

in _Host.cshtml

```
<script>
window.onload = function (){
 eventHandler = function (e){
         
            DotNet.invokeMethodAsync('jsInteropTest', 'jsKeyHandler',e.keyCode);
        
  }
  window.addEventListener('keydown', eventHandler, false);
}
</script>
 ```
 
 In MainLayout.razor
 ```
  public string jsKey { get; set; }
    private static Func<string, Task> KeyDownAction;

    private async Task LocalKeyDownAction(string value)
    {
        jsKey = value;    
        await InvokeAsync(StateHasChanged); 

    }

    [JSInvokable("jsKeyHandler")]
    public static async Task jsKeyHandler(object text)
    {
         await KeyDownAction(text.ToString());
    
    }
   protected override void OnInitialized()
    {
        KeyDownAction = LocalKeyDownAction;
  
    }
 ```
 
 ```
 
 ```
