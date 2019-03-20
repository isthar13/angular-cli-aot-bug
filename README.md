# AngularCliAotBug

This project is a demo to show an error detected using ng serve with AOT enabled.

## Environment
The app.component.html uses a variable that doesn't exists in app.component.ts: {{missingVariable}}.
If you compile the project with AOT enabled an error is shown: ERROR in src/app/app.component.html(3,7): : Property 'missingVariable' does not exist on type 'AppComponent'.

## Problem
The problem using ng serve is that after this compilation error the files are not refreshed after changes with the server running. So although you remove the {{missingVariable}} to fix the compilation error, the server is not reloaded.

Step by step:
1. Run ng serve.
2. See the compilation error.
3. Remove the {{missingVariable}} part in app.component.html.

The server is not reloaded, it doesn't refresh after the changes.
The expected behaviour is the server refreshing after saving changes.

I have found that if the first time you run ng serve there are no compilation errors, and later some compilation error occurs, when you add more changes to the files the server reloads fine.

Step by step:
1. Remove the {{missingVariable}} part in app.component.html.
2. Run ng serve.
3. See no compilation errors.
4. Add {{missingVariable}} again to app.component.html.
5. See the compilation error.
6. Remove the {{missingVariable}} part in app.component.html once more.
7. See the server has reloaded with no compilation error.

This is the expected behaviour when after ng serve some compilation error occurs.
