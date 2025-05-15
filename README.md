# SOAP-based Web Services

## Aim

To create SOAP-based web services using both server-side and client-side implementations.

## Procedure

### Server-Side Implementation

1. **Open NetBeans IDE:**
   - Launch NetBeans IDE on your machine.

2. **Create a New Project:**
   - Click `File` -> `New Project`.
   - Choose `Java Web` and then `Web Application`, and click `Next`.

3. **Configure Project:**
   - Provide a suitable name for your project and click `Next`.
   - Select `GlassFish Server` as the server and `Java EE 7 Web` as the Java EE version. Click `Finish`.

4. **Create a New Web Service:**
   - Right-click your project in the Projects tab and select `New` -> `Web Service`.

5. **Define Web Service:**
   - In the new window, give your web service a name and package name. Click `Finish`.

6. **Add Operation:**
   - Right-click on your web service under the “Web Services” folder in your project and select `Add Operation`.
   - In the window that appears, provide a name and return type for the operation. Click `Add` to define parameters (for demonstration, use two parameters). Click `OK`.

7. **Implement Operation:**
   - NetBeans will generate a skeleton for the operation. Replace `return 0.0` with `return (a+b)` to perform addition.
   - Save your project, right-click on it, and select `Clean and Build`. Then, right-click again and select `Deploy`.

8. **Test Web Service:**
   - Once deployed, right-click on the web service name and select `Test Web Service`.
   - A new browser window will appear where you can input values to test the web service.

### Client-Side Implementation

1. **Create a New Java Web Project:**
   - Follow steps 1-5 of the server-side section to create a new Java Web Project.

2. **Add Web Service Client:**
   - Right-click on your project and select `New` -> `Web Service Client`.
   - In the window that appears, select `Project` under “Specify the WSDL file of the Web Service” and click `Browse`.

3. **Select Web Service:**
   - Choose the appropriate web service and click `OK`.
   - Fill in the project file with the location of the WSDL file and provide a package name if desired. Click `Finish`.

4. **Verify and Build:**
   - The client will gather the available operations. Ensure “BUILD SUCCESSFUL” appears in the Output Window.

5. **Create JSP Page:**
   - Right-click on `Web Pages` under your project and select `JSP`.
   - Provide a name for your JSP page and click `Finish`.

6. **Invoke Web Service:**
   - Expand the folder `Web Service References` -> `Addition` -> `Addition` -> `AdditionPort`.
   - Drag and drop the `add` operation into the JSP page. NetBeans will auto-generate the code for invoking this operation.

7. **Run JSP Page:**
   - Provide values for the arguments and run the JSP file.
   - A new browser window will display the output of the web service invocation.

8. **Client-Side Remote Invocation (Optional):**
   - Follow steps 1-2 as in the client-side section.
   - Select `WSDL URL` and type the URL of the web service’s WSDL file (e.g., `http://ip:8080/Proj_name/Webservice_name?wsdl`).
   - Complete the remaining procedure as outlined.

## PROGRAM:
# SERVICE
```
Cal-service (JAVA file)

* To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package example;

import javax.jws.WebService;
import javax.jws.WebMethod;
import javax.jws.WebParam;

/**
 *
 * @author SEC
 */
@WebService(serviceName = "Calservice")
public class Calservice {

    /**
     * This is a sample web service operation
     */
    @WebMethod(operationName = "hello")
    public String hello(@WebParam(name = "name") String txt) {
        return "Hello " + txt + " !";
    }

    /**
     * Web service operation
     */
    @WebMethod(operationName = "AddNumbers")
    public Integer AddNumbers(@WebParam(name = "num1") int num1, @WebParam(name = "num2") int num2) {
        //TODO write your implementation code here:
        return (num1 + num2);
    }
}
```
# CLIENT
# index.html
```
<!DOCTYPE html>
<!--
To change this license header, choose License Headers in Project Properties.
To change this template file, choose Tools | Templates
and open the template in the editor.
-->

<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Web Service Client</title>
    </head>
    <body>
        <h1>Addition Web Service</h1>
        
        <!-- Form for user input -->
        <form method="post" action="index.jsp">
            <label for="num1">Number 1:</label>
            <input type="number" id="num1" name="num1" required><br><br>
            
            <label for="num2">Number 2:</label>
            <input type="number" id="num2" name="num2" required><br><br>
            
            <label for="message">Enter a String:</label>
            <input type="text" id="message" name="message" required><br><br>

            <input type="submit" value="Add and Send String">
        </form>
    </body>
</html>
```
# index.jsp
```
<%@page contentType="text/html" pageEncoding="UTF-8"%>
<%@taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>

<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
        <title>Output Page</title>
    </head>
    <body>
        <h1>Web Service Client - Result</h1>

        <%-- Retrieve form values --%>
        <%
            String num1Str = request.getParameter("num1");
            String num2Str = request.getParameter("num2");
            String message = request.getParameter("message");

            int num1 = 0;
            int num2 = 0;
            String resultStr = "";
            String responseMessage = "";

            try {
                // Convert numbers from string to integer
                if (num1Str != null && num2Str != null) {
                    num1 = Integer.parseInt(num1Str);
                    num2 = Integer.parseInt(num2Str);
                }

                // Call the web service to add numbers
                example.Calservice_Service service = new example.Calservice_Service();
                example.Calservice port = service.getCalservicePort();

                // Web service call for addition
                int result = port.addNumbers(num1, num2);
                resultStr = " " + result;

                // Web service call for string message
                if (message != null && !message.isEmpty()) {
                    responseMessage = port.hello(message);
                }

            } catch (Exception e) {
                resultStr = "Error: " + e.getMessage();
            }
        %>

        <%-- Display the result for addition --%>
        <p><b>Result of Addition:</b> <%= resultStr %></p>

        <%-- Display the response message from the web service --%>
        <p><b>Response from Web Service :</b> <%= responseMessage %></p>

    </body>
</html>
```
## OUTPUT 

## Server-Side Implementation

## Server-Side Terminal
![EXPERIMENT 3](https://github.com/user-attachments/assets/3d2fd65e-f466-42ee-bf3d-01f05eaa019e)
## Server-side output pages
## Input page
![EXPERIMENT 2(1)](https://github.com/user-attachments/assets/543bff6a-dfbe-4792-b680-b94cce71c6df)

## Addition output
![EXPERIMENT 2(2)](https://github.com/user-attachments/assets/aa6c6ab6-b136-494b-9289-22818e444fa2)

## Result

The SOAP-based web services were successfully created and executed, demonstrating both server-side and client-side implementations.

