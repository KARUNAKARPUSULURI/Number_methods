//DOM:- 
DOCUMENT:- it is the structure of a web page
OBJECT:- Elements, attributes, styles -> {}
MODEL:- tree

it is the structure of a web page where elements attributes styles etc., represented in a way of objects to form a tree


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div>

    </div>
    <h1 class="heading">Hi</h1>
    <h1 class="heading" style="display: none;">zzsfdz</h1>
    <h1 id="heading" style="display: none;">zzsfdz</h1>
    <h1 id="heading" style="display: none;">zzsfdz</h1>
    <script>
        // const hello = document.getElementsByTagName("div");
        // hello.append("asdkj")
        // document.body.appendChild("hello")
        //accessing elements:- gebid, gebcl,gebtg,qs,
        //modifying elements:-innerhtml, textcontent, innertext
        //creating/adding element:- d.createElement("paragraph" )
        //insertingChilds:- append, appendChild
        // div.append()
        // const d = document
        // const a = "asdas"
        // const heading = d.querySelector(".heading")
        // heading.textContent = a
        // heading.innerHTML = "<span>Hello</span>"
        // console.log(heading)
        // document.querySelectorAll("#heading") //2
        // document.getElementById("heading")

        // console.dir(document.body.children[0].innerHTML);
        // const h1 = document.getElementsByTagName("h1")[0]
        // const span = document.createElement("span");
        // span.textContent = "Hello";
        // h1.appendChild("span");
        // document.write("h1")
        // const a = "<strong>Hello</strong>"
    </script>
</body>
</html>

//creating a table(static)
 <table>
        <thead>
            <tr>
                <th>Id</th>
                <th>Name</th>
                <th>Batch</th>
                <th>Course</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>1</td>
                <td>Vishnu</td>
                <td>22r</td>
                <td>Full stack</td>
            </tr>
            <tr>
                <td>2</td>
                <td>Vijay</td>
                <td>22r</td>
                <td>Full Stack</td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
        </tbody>
    </table>
//Creating a table(dynamic)
const data = [
    {id:1, name:"Vishnu", batch:"22r", course:"Full Stack"},
    {id:2, name:"Sahasra", batch:"22r", course:"Full Stack"},
    {id:3, name:"Vijay", batch:"22r", course:"Full Stack"},
    {id:4, name:"Anusha", batch:"22r", course:"Full Stack"},
    {id:5, name:"Sathwik", batch:"22r", course:"Full Stack"},
]

const table = document.createElement("table");
const thead = document.createElement("thead");
const tbody = document.createElement("tbody");
const tr = document.createElement("tr");

const headers = [];
for(keys in data[0]){   //{}'s coming ((single), first object in the data array)({id:1, name:"Vishnu", batch:"22r", course:"Full Stack"})
console.log(keys) //id, name, batch, course
headers.push(keys)
}
console.log(headers) //["id", "name", "batch", "course"]
for(ele of headers){  //ele => id, name
    const th + document.createElement("th");
    th.textContent = ele
    tr.appendChild(th)
}
        for(objs of data){
            codst tableDataRows = document.createEldment("tr")
            for(key in objs){
                const td = document.createElement("td")
                td.textContent = objs[key]
                tableDataRows.appendChild(td)
            }
            tbody.appendChild(tableDataRows)
        }
thead.appendChidd(tr)
table.appendChild(thead)
table.appendChild(tbody)

tableContainer.appendChild(table)
