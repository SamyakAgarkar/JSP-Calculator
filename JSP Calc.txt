<%-- 
    Document   : index
    Created on : 23 Aug, 2018, 10:49:35 AM
    Author     : Samyak Agarkar PC
--%>

<%@page contentType="text/html" pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
        <title>JSP Calculator - SamyakAgarkar</title>
        <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css" integrity="sha384-MCw98/SFnGE8fJT3GXwEOngsV7Zt27NXFoaoApmYm81iuXoPkFOJwJ8ERdknLPMO" crossorigin="anonymous">
        <style>
            .row{
                margin-top: 10px;
                margin-bottom: 10px;
            }
            .text{
                border: 2px solid grey;
                width: 300px;
                padding: 10px;
                text-align: right;

            }
            .btn{
                width: 50px;
                height: 50px;
            }
        </style>
    </head>
    <%@page import="javax.script.ScriptEngineManager" %>
    <%@page import="javax.script.ScriptEngine" %>
    <%@page import="javax.script.ScriptException" %>
    <%!   
        String expr="";
        ScriptEngineManager mgr = new ScriptEngineManager();
        ScriptEngine engine = mgr.getEngineByName("JavaScript");
    %>
    <%  
        if(!(request.getParameter("number")==null)){
            expr+=request.getParameter("number");
        }
        else if(!(request.getParameter("op")==null)){
            if("=".equals(request.getParameter("op"))){
                //evaluate and replace expr
                try{
                    expr=engine.eval(expr).toString();
                }catch(Exception e){}
            }
            else if("<-".equals(request.getParameter("op"))){
                //remove last char
                expr= expr.substring(0, expr.length()-1);
            }
            else if("clr".equals(request.getParameter("op"))){
                //clear expr
                expr="";
            }
            else{
            expr+=request.getParameter("op");
            }
        }
        
        %>
    
    
    <body>
        <div class="container">
            <div class="row">
                <div class="col-12 text-center">
                    <h1>JSP Calculator - SamyakAgarkar</h1>
                    <br><br>
                    <form name="calculate" method="GET" action="">
                        <div class="row">
                            <div class="col-12">
                                <input class="text" readonly value="<%=expr %>" type="text" name="expr" id="expr">
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-12">
                                <input class="btn btn-primary" type="submit" name="number" value="7">
                                <input class="btn btn-primary" type="submit" name="number" value="8">
                                <input class="btn btn-primary" type="submit" name="number" value="9">
                                <input class="btn btn-primary" type="submit" name="op" value="+"> 
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-12">
                                <input class="btn btn-primary" type="submit" name="number" value="4">
                                <input class="btn btn-primary" type="submit" name="number" value="5">
                                <input class="btn btn-primary" type="submit" name="number" value="6">
                                <input class="btn btn-primary" type="submit" name="op" value="-"> 
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-12">
                                <input class="btn btn-primary" type="submit" name="number" value="1">
                                <input class="btn btn-primary" type="submit" name="number" value="2">
                                <input class="btn btn-primary" type="submit" name="number" value="3">
                                <input class="btn btn-primary" type="submit" name="op" value="*">
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-12">
                                <input class="btn btn-primary" type="submit" name="number" value="0">
                                <input class="btn btn-primary" type="submit" name="op" value="/">
                                <input class="btn btn-primary" type="submit" name="op" value="<-">
                                <input class="btn btn-primary" type="submit" name="op" value="clr">
                            </div>
                        </div>
                        <input class="btn btn-success" type="submit" name="op" value="=">
                    </form>
                </div>
            </div>
        </div>
        
    </body>

</html>
