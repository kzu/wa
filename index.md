---
layout: page
---

Te pasaron un numero de celular para hablar por WhatsApp pero no querés agregarlo a tus contactos?
Copiá el número abajo y te mandamos a WhatsApp directo:

<!-- why this table has a order? -->
<form id="wa" action="" onsubmit="go()" method="GET">
    <table>
        <tr style="border: none !important; ">
            <td style="width: 100%;">
                <input id="phone" onpaste="pasted()" onchange="go()" placeholder="Número de celular, con o sin espacios o guiones, con o sin el prefijo 11 (Bs.As.)" style="width: 100%;">
            </td>
            <td style="width: 1%">
                <button id="chat" type="submit" class="btn btn-green">Chatear</button>
            </td>
        </tr>
    </table>
</form>

<script>
    // on document loaded, check if the URL has a query parameter and if so, set the value of the input field
    document.addEventListener("DOMContentLoaded", function () {
        if (window.location.search.startsWith('?')) {
            document.getElementById("phone").value = window.location.search.substring(1);
            document.getElementById('chat').click();
        }
    });

    function pasted() {
        setTimeout(() => document.getElementById('chat').click(), 0); 
    }

    function go() {
        var phone = document.getElementById("phone").value;
        if (phone.length == 0) {
            setStatus("");
            return;
        }
        // remove all non-numeric characters
        phone = phone.replace(/\D/g, '');
        // if phone starts with 15, remove it
        if (phone.startsWith("15")) {
            phone = phone.substring(2);
        }
        if (phone.length == 8) {
            phone = "11" + phone;
        }
        phone = "+54" + phone;
        var url = "https://wa.me/" + phone;
        document.getElementById("wa").action = url;
        // window.location.href = url;
    }

</script>