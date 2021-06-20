Facts
======


Now let collect facts from a F5 and store those facts into a json file.

We will need to make a new entry into our inventory file:

.. code-block:: yaml 
   :caption: inventory group adc

    [adc]
    BigIp1 ansible_host=


.. code-block:: yaml
   :caption: f5.yml 


    ---
    - name: F5 Facts 
      hosts: [adc]
      gather_facts: false
      connection: local
    
      vars:
        provider:
           server: 
           user: "f5guest"
           password: ""
           validate_certs: no  

      tasks:

      - name: Gather F5 Info
        bigip_device_info:
          provider: "{{ provider }}"
          gather_subset:
            - all
        delegate_to: localhost
        register: bigip_fact_out

      - name: Copy facts to file
        copy:
          dest: facts.json
          content: "{{ bigip_fact_out }}"
