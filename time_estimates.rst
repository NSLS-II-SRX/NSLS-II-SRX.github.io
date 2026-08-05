Estimating Scan Times
===================

xrf_map
*******
.. raw:: html

   <style>
       /* Removes increment arrows for Chrome, Safari, Edge, and Opera */
       input::-webkit-outer-spin-button,
       input::-webkit-inner-spin-button {
           -webkit-appearance: none;
           margin: 0;
       }

       /* Removes increment arrows for Firefox */
       input[type=number] {
           -moz-appearance: textfield;
       }

       /* Container to stack label above input and keep them side-by-side */
       .input-group {
           display: inline-block;
           margin-right: 15px;
           vertical-align: bottom;
       }

       /* Style for the text labels */
       .input-group label {
           display: block;
           font-size: 13px;
           margin-bottom: 4px;
           font-weight: bold;
       }
   </style>

   <div style="background-color: #fafafa; border: 1px solid #e1e4e6; border-radius: 8px; padding: 24px; margin: 24px 0; max-width: 450px; box-shadow: 0 2px 5px rgba(0,0,0,0.05);">

      <h5 style="margin-top: 0; margin-bottom: 15px; font-size: 14px; font-weight: bold; border-bottom: 1px solid #eee; padding-bottom: 6px;">
      Time Estimate
      </h5>
      
      <!-- Input 1 Group -->
      <div class="input-group">
         <label>xnum (int)</label>
         <input type="number" id="val1" min="0" step="1" placeholder="0" oninput="calc()" style="border: 1px solid #ccc; border-radius: 4px; padding: 6px 10px; width: 90px; box-sizing: border-box;">
      </div>

      <!-- Input 2 Group -->
      <div class="input-group">
         <label>ynum (int)</label>
         <input type="number" id="val2" min="0" step="1" placeholder="0" oninput="calc()" style="border: 1px solid #ccc; border-radius: 4px; padding: 6px 10px; width: 90px; box-sizing: border-box;">
      </div>

      <!-- Input 3 Group -->
      <div class="input-group">
         <label>dwell (sec)</label>
         <input type="number" id="val3" min="0" step="any" placeholder="0.0" oninput="calc()" style="border: 1px solid #ccc; border-radius: 4px; padding: 6px 10px; width: 90px; box-sizing: border-box;">
      </div>
      
      <!-- Checkbox Group aligned to the bottom with the inputs -->
      <div class="input-group">
         <label>fly_on_y</label>
         <div style="display: flex; align-items: center; height: 30px;">
            <input type="checkbox" id="toggleBtn" onchange="calc()" style="margin: 0; width: auto;">
            <span style="font-size: 13px; margin-left: 5px; font-weight: bold; white-space: nowrap;"></span>
         </div>
      </div>

      <div style="margin-bottom: 10px;"></div>

      <div style="text-align: right; display: flow-root;">
         <!-- Left-aligned result text on the same line -->
         <span style="float: left; font-weight: bold; font-size: 16px; line-height: 28px;">
            Result: <span id="res">0 sec</span>
         </span>
      </div>

   </div>

   <script>
   function calc() {
       var v1 = Math.max(1, Math.floor(parseInt(document.getElementById('val1').value) || 0));
       var v2 = Math.max(1, Math.floor(parseInt(document.getElementById('val2').value) || 0));
       var v3 = Math.max(0, parseFloat(document.getElementById('val3').value) || 0);

       var fly_on_y = document.getElementById('toggleBtn').checked;

       var row_overhead = 0;
       if (fly_on_y) {
         row_overhead = v1 * 4
      } else {
         row_overhead = v2 * 4
      }

      var res_sec = 10 + (v1 * v2 * v3) + row_overhead;
      var res_text = "";

      // Dwell issue
      if (v3 == 0) {
         res_sec = 0
      }

      // Time reporting logic
      if (res_sec < 60) {
         // Round to 1 decimal place if it's a float
         res_text = Math.round(res_sec) + " sec";
      } else if (res_sec < 3600) {
         var res_min = Math.floor(res_sec / 60);
         var remaining_sec = Math.round(res_sec % 60);
         res_text = res_min + " min and " + remaining_sec + " sec";
      } else {
         var res_hr = Math.floor(res_sec / 3600);
         var remaining_sec = res_sec % 3600;
         var res_min = Math.round(remaining_sec / 60);
         res_text = res_hr + " hr and " + res_min + " min";
      }

      document.getElementById('res').innerText = res_text;
   }
   </script>


