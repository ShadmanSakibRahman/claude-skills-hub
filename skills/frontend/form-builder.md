---
description: Generate complex forms with validation, multi-step wizards, dynamic fields, and accessibility
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in building production-grade forms for web applications. When this skill is invoked, do the following:

1. Ask the user what form they need (or infer from context). Clarify:
   - What fields are required and their types
   - Whether it is a single-step or multi-step wizard
   - What happens on submission (API call, local state update, file upload)
   - Any conditional/dynamic field logic
2. Read the existing project to determine the form approach:
   - Check for existing form libraries (React Hook Form, Formik, VeeValidate)
   - Check for validation libraries (Zod, Yup, Joi, Valibot)
   - Identify UI component library for form inputs (Shadcn, MUI, Ant Design, Headless UI)
   - Look at existing form patterns in the codebase for consistency

3. Set up the form with the appropriate library:

   **React Hook Form (preferred for React):**
   - Initialize with `useForm` and typed `DefaultValues`
   - Configure `mode: 'onBlur'` for validation on field blur (best UX balance)
   - Use `register` for simple inputs or `Controller` for complex/custom inputs
   - Implement `useFieldArray` for dynamic repeatable field groups
   - Use `watch` and `useWatch` for fields that affect other fields conditionally
   - Handle submission with `handleSubmit` wrapping an async submit function

   **Formik (if project uses it):**
   - Set up with `useFormik` hook or `<Formik>` component
   - Use `<Field>` and `<ErrorMessage>` components for consistency
   - Implement `FieldArray` for dynamic fields

4. Define validation schema:

   **With Zod (preferred):**
   - Create a Zod schema that matches the form shape exactly
   - Use `z.string().min(1, 'Required')` instead of just `z.string()` for required fields
   - Add `.email()`, `.url()`, `.regex()` for format validation
   - Use `z.discriminatedUnion` for fields that depend on a type selector
   - Use `.refine()` and `.superRefine()` for cross-field validation (password confirmation, date ranges)
   - Infer the TypeScript type from the schema with `z.infer<typeof schema>`
   - Connect to React Hook Form via `zodResolver`

   **With Yup (if project uses it):**
   - Create a Yup schema with `.required()`, `.email()`, `.min()`, `.max()`
   - Use `.when()` for conditional validation
   - Connect via `yupResolver`

5. Build the form UI with proper structure:
   - Wrap each field in a labeled group: `<label>` + `<input>` + error message
   - Use `htmlFor`/`id` pairing for every label-input connection
   - Mark required fields visually (asterisk) and programmatically (`aria-required`)
   - Display validation errors inline below each field with `aria-describedby`
   - Use `aria-invalid="true"` on fields with errors
   - Add `autocomplete` attributes for all standard fields (name, email, address, phone, etc.)
   - Group related fields with `<fieldset>` and `<legend>` (e.g., address fields, payment details)

6. Implement multi-step wizard (if applicable):
   - Create a `steps` configuration array with step metadata (title, description, fields, schema)
   - Track current step index in state
   - Validate only the current step's fields before advancing
   - Persist partial form data across steps (keep in form state, not submitted until final step)
   - Show a progress indicator (step numbers, progress bar, or breadcrumb trail)
   - Allow navigating back to previous steps without losing data
   - Submit all accumulated data on the final step
   - Handle browser back button / route changes gracefully (warn about unsaved progress)

7. Handle dynamic fields:
   - Use `useFieldArray` for add/remove field groups (e.g., adding multiple addresses, phone numbers)
   - Implement conditional fields that show/hide based on other field values
   - Update validation schema dynamically when fields appear/disappear
   - Maintain proper field registration when fields are conditionally rendered

8. Implement form submission:
   - Disable the submit button during submission (prevent double-submit)
   - Show a loading indicator on the submit button
   - Handle API errors: map server-side field errors to `setError` on specific fields
   - Show a success state (toast notification, redirect, or inline confirmation)
   - Reset the form after successful submission if appropriate
   - Implement retry logic for transient failures

9. Add user-experience enhancements:
   - Debounce async validation (username availability, email uniqueness) with 300-500ms delay
   - Show character counts for fields with max length
   - Auto-format fields where appropriate (phone numbers, credit cards, dates)
   - Implement unsaved changes detection with a leave-page warning (`beforeunload`)
   - Support paste handling for multi-field inputs (e.g., pasting full address)

Best practices to follow:
- Validate on blur for the first interaction, then on change after the first error (progressive validation)
- Never clear the entire form on a validation error
- Keep forms short: ask only what is needed, use progressive disclosure for optional fields
- Provide clear, specific error messages (not just "Invalid field")
- Test form with keyboard only: Tab between fields, Enter to submit, Escape to cancel
- Support form autofill by using correct `name` and `autocomplete` attributes

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
