<!--    Note employee-table in kebab-case, the convention for html 
        File name and import are in PascalCase, convention for JS.
-->

<!-- A template can only have one child element.  While the <div> isn't strictly
        necessary it makes it easy to add additional components going forward.
-->

<template>
    <div id="employee-table">
        <table>
            <thead>
                <tr>
                    <th>Employee name</th>
                    <th>Employee email</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>Old King Cole</td>
                    <td>okc@merryoldsoul.com</td>
                </tr>
                <tr>
                    <td>The Mouse</td>
                    <td>micky@theclock.com</td>
                </tr>
                <tr>
                    <td>Sir H. Dumpty, Esq.</td>
                    <td>humpty@thewall.com</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>


<script>
    export default {
        name: 'employee-table'
    }
</script>

<style scoped></style>