---
layout: page
---

Te pasaron un numero de celular para hablar por WhatsApp pero no querés agregarlo a tus contactos?
Copiá el número abajo y te mandamos a WhatsApp directo:

<!-- why this table has a order? -->
<table>
    <tr style="border: none !important; ">
        <td style="width: 100%;">
            <input id="phone" style="width: 100%;">
        </td>
        <td style="width: 1%">
            <button onclick="go()" class="btn btn-green">Chatear</button>
        </td>
    </tr>
</table>

<p id="status" style="display: none;">
</p>

<p id="reader" style="display: none;">
</p>

<script>
    // on document loaded, check if the URL has a query parameter and if so, set the value of the input field
    document.addEventListener("DOMContentLoaded", function () {
        
        if (window.location.search.startsWith('?')) {
            document.getElementById("phone").value = window.location.search.substring(1);
            go();
        }
    });

    function setStatus(text) {
        document.getElementById("status").innerHTML = text;
        if (text.length > 0) {
            document.getElementById("status").style.display = "block";
        } else {
            document.getElementById("status").style.display = "none";
        }
    }

    function go() {
        setTimeout(async () => {
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
            window.location.href = url;
        }, 0);
    }

</script>