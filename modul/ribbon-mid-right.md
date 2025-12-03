# Ribbon (Mid-Right)

![UiTM Main Page](../images/modul/ribbon-mid-right.webp ":size=100%")

Ribbon ini boleh digunakan sebagai visual promosi kepada sesuatu peristiwa. Ribbon ini melekat ke bahagian _sidebar_ kanan tengah laman web. Untuk mencipta modul ribbon seperti diatas, ikuti langkah berikut:

<ol>
    <li>Nyah aktif Default Editor</li>
        <ol type="a">
            <li>System - Global Configuration</li>
            <li>Site - Default Editor - None (Sekiranya tidak tukar, TinyMCE Editor adalah WYSIWYG Editor dan kod HTML dan CSS ribbon tidak akan berfungsi)</li>
            <li>Save and Close</li>
        </ol>
    <li>Muat naik side riboon</li>
        <ol type="a">
            <li>Menu Content - Media</li>
            <li>Create New Folder: ribbon </li>
            <li>Muat naik ribbon (format .png) </li>
        </ol>
    <li>Content - Site Module</li>
    <li>New - Custom</li>
    <li>Title - Mid Ribbon</li>
    <li>Title - Hide</li>
    <li>Position - Debug (Position debug akan wujud disemua halaman)</li>
    <li>Salin dan tampal kod dibawah (tukar parameter fail imej ribbon sekiranya berbeza)</li>
    <li>Save and Close</li>
</ol>

> Jangan lupa untuk pastikan anda memilih menu yang diperlukan untuk paparan modul ini di **Menu Assignment**

```html
<style>
  .ribbon-right {
    position: fixed;
    /* fixed or absolute */
    right: 0;
    top: 50%;
    transform: translateY(-50%);
    z-index: 1030;
    max-height: 10vh;
  }
</style>

<img src="images/ribbon/ribbon-side.png" alt="Ribbon" class="ribbon-right" />
```
