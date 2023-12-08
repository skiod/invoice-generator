<template>
  <div>
      <div class="flex-container">

    <!-- invoice generator -->
    <section style="flex-grow: 4;">
      <div class="container">

        <div class="invoice" id="invoice-container" @click="handleClick">
          <div class="row">
            <div class="col-7 mb-2" data-invoicly="true" data-only-settings="true">
              <img alt="Logo" id="uploadedLogo" src="https://fakeimg.pl/600x400?text=Logo" class="logo">
              <form id="logoForm">
                <input type="file" accept="image/*" id="logoInput" @change="handleLogoChange()">
              </form>

            </div>
            <div class="col-5">
              <h1 class="document-type display-4">
                <div data-invoicly="true">FACTURE</div>
              </h1>
              <div class="text-right" data-invoicly="true">N°90T-17-01-0123</div>
            </div>
          </div>
          <div class="row">
            <div class="col-7">
              <div data-invoicly="true">90TECH SAS</div><br>
              <div data-invoicly="true">
                6B Rue Aux-Saussaies-Des-Dames <br> 57950 MONTIGNY-LES-METZ
              </div>

            </div>
            <div class="col-5" style="text-align: right;">
              <br><br><br>
              <div data-invoicly="true">
                Energies54 <br>
                Réf. Client C00022 <br>
                12 Rue de Verdun <br>
                54250 JARNY</div>
            </div>
          </div>
          <br>
          <br>
          <h6>
            <div data-invoicly="true">Audits et rapports mensuels (1er Novembre 2016 - 30 Novembre 2016)</div>
          </h6>
          <br>
          <table id="table" class="table table-striped">
            <thead>
              <tr>
                <th data-invoicly="true">Description</th>
                <th data-invoicly="true">Quantité</th>
                <th data-invoicly="true">Unité</th>
                <th data-invoicly="true">PU HT</th>
                <th data-invoicly="true">TVA</th>
                <th data-invoicly="true">Total HT</th>
                <th class="hide-elements">Action</th>

              </tr>
            </thead>
            <tbody>
              <tr v-for="(row, index) in rows" :key="index">
                <td><span :data-invoicly-field="'description'" :data-invoicly-row-id="index" :data-invoicly="true">{{ row.description }}</span></td>
                <td><span data-invoicly-field="quantity" :data-invoicly-row-id="index" :data-invoicly="true" data-invoicly-type="number">{{ row.quantity }}</span></td>
                <td><span data-invoicly-field="unity" :data-invoicly-row-id="index" :data-invoicly="true">{{ row.unity }}</span></td>
                <td><span data-invoicly-field="puHT" :data-invoicly-row-id="index" :data-invoicly="true" data-invoicly-type="number">{{ row.puHT }}</span> {{currency}}</td>
                <td><span data-invoicly-field="tva" :data-invoicly-row-id="index" :data-invoicly="true" data-invoicly-type="number">{{ row.tva }}</span>%</td>
                <td><span data-invoicly-field="totalHT" :data-invoicly-row-id="index" :data-invoicly="true" data-invoicly-type="number">{{ row.totalHT }}</span> {{currency}}</td>
                <td>
                  <button class="btn btn-sm btn-danger" @click="deleteRow(index)">-</button>
                </td>
              </tr>
            </tbody>

          </table>
          <button style="display:block;text-align:right" class="btn btn-xs btn-success" @click="addNewRow()">+</button>

          <div class="row">
            <div class="col-8">
            </div>
            <div class="col-4">
              <table class="table table-sm text-right">
                <tbody>
                  <tr>
                    <td><strong>Total HT</strong></td>
                    <td class="text-right" id="total-ht">{{totalHT.toFixed(2)}} {{currency}} </td>
                  </tr>
                  <tr>
                    <td>TVA 20%</td>
                    <td class="text-right" id="total-tva">{{totalTVA.toFixed(2)}} {{currency}} </td>
                  </tr>
                  <tr>
                    <td><strong>Total TTC</strong></td>
                    <td class="text-right" id="total-ttc">{{totalTTC.toFixed(2)}} {{currency}} </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>

          <div class="conditions" data-invoicly="true">
            En votre aimable règlement
            Et avec nos remerciements. <br>
            Conditions de paiement : paiement à réception de facture, à 15 jours. <br>
            Aucun escompte consenti pour règlement anticipé. <br>
            Règlement par virement bancaire. <br>

            En cas de retard de paiement, <br> indemnité forfaitaire pour frais de recouvrement : 40 euros (art. L.4413
            et L.4416s
            code du commerce).

          </div>

          <br>
          <br>
          <br>
          <br>

          <div  class="bottom-page text-right" data-invoicly="true">
            90TECH SAS - N° SIRET 80897753200015 RCS METZ <br>
            6B, Rue aux Saussaies des Dames - 57950 MONTIGNY-LES-METZ 03 55 80 42 62 - www.90tech.fr <br>
            Code APE 6201Z - N° TVA Intracom. FR 77 808977532 <br>
            IBAN FR76 1470 7034 0031 4211 7882 825 - SWIFT CCBPFRPPMTZ <br>
          </div>

        </div>
      </div>
    </section>

    <!-- settings -->
    <section class="hide-elements" style="flex-grow: 2;">
      <h4 class="text-center">Settings</h4>
      <table class="table">
        <tbody>
          <tr>
            <td><strong>Currency:</strong></td>
            <td>
              <select v-model="currency" id="select-currency" class="form-select">
                <option value="$">USD ($)</option>
                <option value="€">EUR (€)</option>
                <option value="£">GBP (£)</option>
                <option value="dh">MAD (dh)</option>
                <!-- Add more currency options as needed -->
              </select>
            </td>
          </tr>
          <tr>
            <td><strong>Show Logo:</strong></td>
            <td>
              <div class="mb-3 form-check">
                <input type="checkbox" id="autoRecalculate" class="form-check-input">
              </div>
            </td>
          </tr>
         
        </tbody>
      </table>
      <button style="display:block;width:100%" class="btn btn-success btn-block" @click="printInvoice()">Print Invoice</button>

      <hr>
      <div v-if="style && showSettings" class="settings-div" id="settingsDiv">
        <div>
          <div class="form-group mb-2">
            <label for="textAlign">Text Align:</label>
            <div style="display:flex;justify-content:space-between">
              <div><i style="cursor:pointer" :style="style.textAlign != 'left' ? 'color:#ddd' : ''" @click="setAlign('left')" class="fa fa-align-left"></i></div>
              <div><i style="cursor:pointer" :style="style.textAlign != 'center' ? 'color:#ddd' : ''" @click="setAlign('center')" class="fa fa-align-center"></i></div>
              <div><i style="cursor:pointer" :style="style.textAlign != 'right' ? 'color:#ddd' : ''" @click="setAlign('right')" class="fa fa-align-right "></i></div>
            </div>
          </div>
    
          <div class="form-group mb-2">
            <label for="backgroundColor">Background Color:</label>
            <input type="color" class="form-control" id="background" @change="backgroundColorChanged()" v-model="style.backgroundColor" name="backgroundColor">
                <p>Selected Color: {{ style.backgroundColor }}</p>
          </div>
    
          <div class="form-group mb-2">
            <label for="color">Text Color:</label>
            <input type="color" class="form-control" id="color" @change="colorChanged()" v-model="style.color" name="color">
          </div>
    
          <div class="form-group mb-2">
            <label for="fontSize">Font Size:</label>
            <input type="number" class="form-control" id="fontSize" v-model="style.fontSize" @change="fontSizeChanged()" name="fontSize" value="16">
          </div>
    
        </div>
      </div>

    </section>

  </div>
  
  </div>
</template>

<script>
export default {
  name: 'Invoice',
  data(){
    return {
      rows: [
        { description: 'Product 1', quantity: 1, unity: 'Unit', puHT: 10, tva: 20, totalHT: 10 },
        { description: 'Product 2', quantity: 2, unity: 'Unit', puHT: 20, tva: 10, totalHT: 40 },
      ],
      style : {
        backgroundColor: '#ffffff',
        color: '#000000',
        fontSize: '16 px',
        textAlign : 'center'
      },
      currency: '$',
      totalHT: 0,
      totalTVA: 0,
      totalTTC: 0,
      showSettings : false,
      selectedElement : null
    }
  },
  methods: {
    handleClick(event) {
      const editableDiv = event.target;

      if (editableDiv.getAttribute('data-invoicly')) {

        this.selectedElement = editableDiv
        //show settings
        this.showSettings = true
        this.style.color = this.rgbaToHex(window.getComputedStyle(editableDiv).color)
        this.style.backgroundColor = this.rgbaToHex(window.getComputedStyle(editableDiv).backgroundColor)
        this.style.fontSize = window.getComputedStyle(editableDiv).fontSize.replace('px','')
        this.style.textAlign = window.getComputedStyle(editableDiv).textAlign

        console.log(window.getComputedStyle(editableDiv).backgroundColor)
        console.log(this.rgbaToHex(window.getComputedStyle(editableDiv).backgroundColor))

        if(editableDiv.getAttribute('data-only-settings')) return

        if (editableDiv.getAttribute('data-invoicly-type') === 'number') {
          this.editNumberField(editableDiv);
        } else {
          this.editTextField(editableDiv);
        }
      }else{
        this.showSettings = false
      }
    },
    rgbaToHex(rgba) {
      // Extract the values of red, green, blue, and alpha from the RGBA string
      const values = rgba.match(/\d+/g);

      // Convert the RGB values to hexadecimal
      const hex = values.slice(0, 3)
        .map(val => Number(val).toString(16).padStart(2, '0'))
        .join('');

      // Convert the alpha value to hexadecimal
      const alphaHex = Math.round(parseFloat(values[3]) * 255).toString(16).padStart(2, '0');

      // Construct the HEX representation with or without alpha
      const hexWithAlpha = values[3] !== undefined ? `#${hex}${alphaHex}` : `#${hex}`;

      return hexWithAlpha.toUpperCase(); // Optionally convert to uppercase
    },
    editNumberField(editableDiv) {
      const inputElement = document.createElement('input');
      inputElement.type = 'number';
      inputElement.min = 0
      inputElement.style.width = editableDiv.offsetWidth * 1.8 + 'px';
      inputElement.value = editableDiv.innerText;
      inputElement.className = 'transparent-input text-right';

      editableDiv.replaceWith(inputElement);

      inputElement.addEventListener('blur', () => {
        editableDiv.innerText = inputElement.value;

        console.log('----',inputElement.value)
        const rowId = editableDiv.getAttribute('data-invoicly-row-id')
        const field = editableDiv.getAttribute('data-invoicly-field')
        console.log(rowId,field)
        if(rowId && field){
          this.rows[rowId][field] = parseFloat(inputElement.value)
        }
        console.log(JSON.stringify(this.rows))
        inputElement.replaceWith(editableDiv);
        this.calculateTotals();
      });

      inputElement.focus();
    },
    editTextField(editableDiv) {
      const inputElement = document.createElement('textarea');
      inputElement.style.height = editableDiv.offsetHeight + 'px';
      inputElement.style.width = editableDiv.offsetWidth * 0.5 + 'px !important';
      inputElement.value = editableDiv.innerText;
      inputElement.className = 'transparent-input text-right';

      editableDiv.replaceWith(inputElement);

      inputElement.addEventListener('blur', () => {

        const rowId = editableDiv.getAttribute('data-invoicly-row-id')
        const field = editableDiv.getAttribute('data-invoicly-field')
        if(rowId && field){
          this.rows[rowId][field] = parseFloat(inputElement.value)
        }

        editableDiv.innerText = inputElement.value;
        inputElement.replaceWith(editableDiv);
        this.calculateTotals();
      });

      inputElement.focus();
    },
    calculateTotals() {
      console.log('calculateTotals triggred')
      this.totalHT = 0;
      this.totalTVA = 0;
      this.totalTTC = 0;

      this.rows.forEach((row) => {
        const { quantity, puHT, tva } = row;

        console.log(quantity,puHT,tva)

        // Calculate total HT for the current row
        const rowTotalHT = quantity * puHT;

        row.totalHT = rowTotalHT
        
        // Update total HT, total TVA, and total TTC
        this.totalHT += rowTotalHT;
        this.totalTVA += rowTotalHT * (tva / 100);
        this.totalTTC += rowTotalHT * (1 + tva / 100);
      });

    },
    addNewRow() {
      const newRow = {
        description: 'New Description',
        quantity: 1,
        unity: 'Unit',
        puHT: 0,
        tva: 0,
        totalHT: 0,
      };

      this.rows.push(newRow);
      this.calculateTotals();
    },   
    deleteRow(index) {
      const isConfirmed = window.confirm("Are you sure you want to proceed?");
      if(isConfirmed){
        this.rows.splice(index, 1);
        this.calculateTotals();
      }
    },
    handleLogoChange() {
      const logoInput = document.getElementById('logoInput');
      const uploadedLogo = document.getElementById('uploadedLogo');

      const file = logoInput.files[0];

      if (file) {
        // Use FileReader to read the selected file
        const reader = new FileReader();

        reader.onload = function (e) {
          // Set the source of the image to the base64-encoded content of the file
          uploadedLogo.src = e.target.result;
        };

        // Read the file as a data URL
        reader.readAsDataURL(file);
      }
    },
    fontSizeChanged(){
      console.log('fontSize changed',this.style.fontSize + 'px')
      this.selectedElement.style.fontSize = this.style.fontSize + 'px'
    },
    colorChanged(){
      this.selectedElement.style.color = this.style.color
    },
    backgroundColorChanged(){
      this.selectedElement.style.backgroundColor = this.style.backgroundColor
    },
    setAlign(where){
      this.style.textAlign = where
      this.selectedElement.style.textAlign = where
    },
    printInvoice() {
      // Implement printInvoice logic
      window.print()
    },
    getSelectedCurrency() {
      // Implement getSelectedCurrency logic
      return '$'; // Replace with your logic to get the selected currency
    },
    applySettings() {
      const parentDiv = document.getElementById('invoice-container');
      this.applySettingsToElement(parentDiv);
    },
    applySettingsToElement(targetDiv) {
      targetDiv.style.backgroundColor = this.backgroundColor;
      targetDiv.style.color = this.color;
      targetDiv.style.fontSize = this.fontSize + 'px';
    },
  },
  watch: {
    'rows': {
      deep: true,
      handler: 'calculateTotals',
    },
  },
  mounted() {
    this.calculateTotals()
  },
}
</script>
